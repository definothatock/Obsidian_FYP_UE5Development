THE AI behaviour consist of 4 main categories (in order):
 - Perception
 - Cache
 - Evaluation
 - Execution

Brief introduction to the categories:
Perception (AI Perception)
The main functionality is provided by engine plugin "AI Perception". Perception provides raw data input for the AI system.

Cache (Working Memory)
The is a data layer that stores parameters of individual Actors. It provides basic queries for Decision making.

Evaluation (Evaluator)
This is the algorithm layer, judge the motivation and booleans via processing entry data from Cache.

Execution (AI State Tree)
This layer that perform actions. Essentially a State Tree that react base on judgments made from previous layer.

so far overall flow:
Perception Input -> Evaluator init MemUpdateContainer based on existence in array -> update other Container data field based on Perception pulse -> finalize update (push Container into InsertOrRefreshEntry) -> Evaluate Entry-Priority/Motivation (need both, not yet planned order/dependency) -> trigger state tree event -> state tree update actions





# some random algo design from AI? huh:

Below is a lightweight foundation you can layer on top of your current Working Memory entries. I’ll keep everything engine‑agnostic enough for Blueprint prototyping, but note where a future C++ helper library can take over.

---

## 1. Normalize the raw data

Before any scoring, convert the heterogeneous entry fields into comparable, 0‑1 (or ‑1–1) signals. A simple helper struct per entry keeps things tidy:

```cpp
struct FPerceptionSignals
{
	float Visibility;      // 0..1   (1 = in LOS & actively sensed)
	float Audibility;      // 0..1   (derived from Hearing strength / falloff)
	float TouchCertainty;  // 0..1   (1 = currently touching/hit)
	float Recency;         // 0..1   (exp(-Δt / RecencyHalfLifeSeconds))
	float DamageFactor;    // 0..1   (AccumulatedDmg / DmgCap)
	float DistanceFactor;  // 0..1   (1 - Clamp(Distance / MaxRange))
	float Confidence;      // 0..1   (see section 3)
	float Opportunity;     // 0..1   (loot, prey, objectives)
	float ThreatBias;      // 0..1   (UniversalThreatLevel mapped to 0..1)
};
```

You already have `FWorkingMemoryScoringWeights`—extend that struct with range caps (e.g. `DamageCap`, `MaxOpportunityRange`, sense falloffs) so both BP and C++ share the same tunables.

---

## 2. Threat score blueprint (foundation)

Threat should feel like “pressure to defend/attack.” Mix static classification with dynamic events:

```
ThreatScore =
    BaseThreat                       // from species table / UniversalThreatLevel
  + wDamage   * DamageFactor
  + wLOS      * Visibility
  + wAudio    * Audibility
  + wTouch    * TouchCertainty
  + wDistance * DistanceFactor       // close targets are threatening
  + wFocus    * TimeAsFirstTarget    // inertia (seconds normalized)
  + wPack     * NearbyAlliesFactor   // optional: more allies => higher threat
```

- Clamp to `[0, 1]`, then rescale to any range you like (e.g. `0..100`).
- `wFocus` gives stickiness—so a currently targeted actor must lose real leverage before you swap. This works with your `SwitchMargin` & `SwitchCooldownSeconds`.

**C++ helper idea:** create `UMemSys_WorkingMemoryScoringLib::ComputeThreat(const FWorkingMemoryEntry&, const FWorkingMemoryScoringWeights&)`. Blueprint can call this per entry after committing updates.

---

## 3. Confidence score

Confidence drives whether the creature is sure enough to act aggressively. Consider the sense history:

```
Confidence =
    wIdentified * IsIdentified
  + wLOS       * Visibility
  + wRecency   * Recency
  + wTriang    * WasPredicted ? 0.2f : 0
  + wNoiseTag  * KnownNoiseSignature ? 0.1f : 0
```

- When `IsActivelySensed` drops, confidence decays using `RecencyHalfLifeSeconds`.
- Feeding “false positives” (e.g. only hearing) should keep confidence below an “engage” threshold, so the AI might stalk or investigate rather than commit.

---

## 4. Opportunity score

Use a symmetric formula but aim it at “reward” rather than “danger”:

```
OpportunityScore =
    BaseOpportunity                 // from subject classification (prey, loot…)
  + wDistance * DistanceFactor      // close edible target => better
  - wThreat  * ThreatScore          // high threat decreases reward
  + wStatus  * (SubjectIsWeakened ? 0.3 : 0)
```

For neutral actors you can keep this near zero.

---

## 5. Motivation vector (Attack / Investigate / Flee / Ignore)

Derive high-level motives by combining Threat, Confidence, Opportunity, and creature temperament slices:

|Motivation|Suggested input|
|---|---|
|**Attack**|`ThreatScore * AggressionTrait * Confidence`|
|**Flee**|`ThreatScore * (1 - Confidence) * SurvivalTrait`|
|**Investigate**|`(1 - Confidence) * (Visibility + Audibility) * CuriosityTrait`|
|**Harvest**|`OpportunityScore * HungerTrait`|
|**Ignore**|fallback (1 – max of others) or tie-breaker|

Store the current dominant motivation alongside the focus entry. Your state tree can subscribe to “motivation changed” events.

---

## 6. Focus selection algorithm

1. **Update entries** (your existing flow).
2. **Score pass**: for every entry, compute Threat, Confidence, Opportunity, Motivation vector. Cache results in the entry to avoid recompute.
3. **Eligibility filters** (cheap, event-driven):
    - Invalid subject → drop.
    - TTL expired → drop.
    - Confidence below threshold → mark as “investigation only.”
4. **Rank candidates**:
    - Primary key: whichever motivation your creature currently prioritizes (e.g. Attack uses Threat).
    - Secondary: recency / switch penalty.
5. **Switch logic**:
    
    ```
    if (BestScore > CurrentScore * (1 + SwitchMargin)
        && TimeSinceLastSwitch > SwitchCooldownSeconds)
    {
        Focus = BestEntry;
        LastSwitchTime = Now;
    }
    ```
    
6. **Emit state tree event** with `FocusSubject`, `Motivation`, `ThreatScore`, etc.

Blueprint prototype: do the scoring inside a `ForEach` loop after `InsertOrRefreshEntry`, then call `SelectFocus`. Later move to C++ (`UMemSys_WorkingMemoryScoringLib::EvaluateEntries(const TArray<FWorkingMemoryEntry>&, ...)`).

---

## 7. Example Blueprint-friendly pseudo flow

1. **Perception pulse** fills `Mem Entry Update Container` (already in your screenshots).
2. When done, call `Commit_WorkMemEntryUpdate`.
3. Immediately after `InsertOrRefreshEntry`, call a new Blueprint function `EvaluateMemoryEntry`:

```
function EvaluateMemoryEntry(Entry, Weights):
    Signals = BuildSignals(Entry, Weights)
    Entry.ThreatScore      = ComputeThreat(Signals, Weights)
    Entry.ConfidenceToSubject = ComputeConfidence(Signals, Weights)
    Entry.OpportunityScore = ComputeOpportunity(Signals, Weights)
    Entry.AttackMotivation = Entry.ThreatScore * Entry.ConfidenceToSubject
    Entry.FleeMotivation   = Entry.ThreatScore * (1 - Entry.ConfidenceToSubject)
    Entry.InvestigateMotivation = (1 - Entry.ConfidenceToSubject) * Signals.Recency
```

4. Store the motivations back into the entry or into a lightweight cache map keyed by `EntryGuid`.
5. Run `SelectFocusFromArray` to apply step 6 above.
6. Broadcast `OnFocusUpdated(FWorkingMemoryEntry, EMotivationType)` to the state tree.

---

## 8. When to move to C++

- **Scoring math** (threat, confidence, opportunity) — no Blueprint loops over dozens of entries each tick.
- **Sorted selection** — implement `SelectFocus` in C++ so you can `TArray::Sort` or use deterministic partial reduce.
- **Decay helpers** — you already plan to move from tick to event-driven; C++ timers or gameplay tasks will help keep costs down.

---

## 9. Extra touches inspired by Rain World / Alien Isolation

|Feature|Implementation idea|
|---|---|
|**Hunting memory**|Add `LastPredictedLocation_Age` to Signals to reward persistent tracking even when unseen.|
|**Sound baiting**|If `Heard` without LOS, bump Investigate motivation but clamp Threat until confirmed.|
|**Fear stacking**|Track `AccumulatedDmgToSelf` vs `Confidence` to trigger panic flee spirals like Rain World.|
|**Ambient distraction**|Inject dummy entries (e.g., loud machinery) with low Threat but high Investigate to pull AI.|

---

## 10. Validating the loop

1. **Unit test** C++ scoring with deterministic entries (use `AutomationSpec`).
2. **Debug draw** overlay: color boxes by dominant motivation (red attack, blue flee, yellow investigate).
3. **Data table** for per-species `FWorkingMemoryScoringWeights` so you can quickly iterate.

---

This should give you a sturdy baseline: a normalized signal layer, a handful of transparent formulas for Threat/Confidence/Opportunity, a motivation vector, and a surgical focus switcher that honors your existing `SwitchMargin` / `SwitchCooldownSeconds`. Start light in Blueprint, then migrate the hot loops into `UMemSys_WorkingMemoryScoringLib` once the behavior feels right.


[[Creature Behaviour Machine]]
[[AI Perceptions]]
[[Working Memory]]