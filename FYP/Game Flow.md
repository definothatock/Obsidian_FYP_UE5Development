# Simple flow
Level start -> scavenge -> Find exit  -> Leave level.
Tarkov/Arc Raider without the unlimited gun, repo/lethal with more map/loot dynamics (hopefully)

## Requirement:
- Hard
	- Scores
		- Can Only Leave with enough Loot/Value. (maybe allow loaning, but only for 1 round?)
		- Can Return to Entrance as fail safe. But some punishment should be introduced (Life Support fee? no map regeneration?) 
- Soft
	- Time
		- **Encourage route commitment, punishes indecision.**
		- As time pass the environment gets harsher
		- Even if time is up, should not be impossible and allows risk runs
	- Exit Locating (optional)
		- **Converts time into information certainty, and creates temporal hub.**
		- Find Radio Radio Infrastructures (more Towers/Emitters help locating Exit better. Maybe fake triangulation?)
		- Radio devices require fixing, and failed fixing might attract hostile creatures / create hazard (should not be too annoying/frequent)
	- Scavenging strategy
		- **Trades coverage for rescue capability.**
		- Player can choose to split up or stay as a pack

Ultimate Balancing Goal: Value vs Time.

### Reasonings for Soft Requirement (Player Decisioning)
What Using Time brings?
- Straightforward: More time to find loot, more time staying in risk.

What Exit Locating (Radio Infrastructure) brings?
- Reduce Time Risk
	- Player can find the exit with 0 clues. But without confirmation, it might take too much time.
	- Activating Radio infrastructures provides levels of guarantees. 
- Reduce Value
	- Finding Radio Devices != finding loot. There might be no loot along the way.
- Utility
	- Can talk to all player from anywhere while using the infrastructure (up to debate)
	- *Need actual testing: Provide limited use device that bring back actually dead player? (too powerful?)*
	- *Up to debate: temporal Value extraction point? reduce the risk of last moment failure?* 
	- *Up to debate:Temporal safe house (if the Infrastructure is a building)* 
- Gameplay anchor
	- Clear Objective for players to plan with. It should be one of the most consistent objective in the entire game.
	- Tower structure provides a solid directional landmark, reduce the frequency of player being 'lost in the wood'.

What Scavenging strategy brings?
- Splitting up
	- Save both Value and Time
		- more squadrons = more coverage running in parallel
	- Risk
		- no helping hands
			- If one is in great risk, they are likely to be out for the round
			- If Recourse / Loot are drop, hard to retrieve for teammates
		- Communication
			- distance groups cannot communicate so easily (Radio emitter limits to Radio Infrastructure / specific loot?)
		- Reformation
			- Require some good planning / resource (flare?), or shouting to mic (this should be allowed because it's funny)
- Stay as a pack
	- Less risk, less coverage.

Extra: What If small number of players (1/2)?
- some balancing required. for now we assume more player, ignores largely.

### Indicator for Time
Not prioritized, but great to have.
Time is the only resource without explicit number indicator. And Since some events are highly tied with time,
to alert player about time/phases (and related events/locations):
- SFX / Music
	- obvious sensory input / mood changer. Good for direct reminder. 
- Lighting
	- Usually are not abrupt and still obvious (day night cycle), but not always applicable. 
- Ambient
	- The least important, as it gives little clues. different background noise that indicate time/events.
	- However, very power at giving subtle clues. 

---
# Thus, Detailed flow:
Level start -> plan scavenging strategy -> Searching (exit && loot)  -> Leave level in time.

## Starting Phase: New Round
- Given per-round Tools (player might have lost it, but always replenish with limited amount each round)
	- to clue Radio device locations (they are clues to the final exit, should not be as vague as the exit)
	- baseline tools (e.g. beacon, for revisiting location? flare for indicating actions?)
- Extra: Select previous saved Loots (utilities)
	- player saved loot is always accessible during setup. 
	- this does not hard contribute to the core game loop, still nice to have.

## Main Phase: Searching
3 main tasks in parallel:
- Resource Management
- Risk and reward (Loot)
- Exit Plan

What possible Resource Management, and Risk and reward to Expect?
- See [[Core mechanics]]: **Resource Management** and **Loot**.

Resource Management
- Medium for Resources?
	- Loot & Weight: Via inventory.
	- Health & Stamina: Via Game Action.
	- Time: Via strategy.

Loot
- How to seek Loot?
	- All scatter around the world / buildings. no exact location, but spawn sockets might be fixed.
- How to tell Value?
	- For simplicity, once collected, all Value should be displayed right away.

Exit Plan
- Either use Radio Infrastructure to location Exit, or directly find the Exit by luck.
- Illusion of choice: Should make players to consider finding Radio Infrastructures often. It provides a very apparent objective (so player doesn't feel lost) and it encourages planned map exploration. 
- Still, there might be way to find the Exit without Radio Infrastructures (using loot utilities?), this allows 'power plays'.

## End Phase 
### option 1: Exiting
The only requirement for entering Exit: Met minimum loot Value as a whole (raw sum), everyone can contribute.
- Meeting the requirement
	- Enter the Final Safe Point
	- Select the loot to pay
	- *Extra, not pioritized: 
		- *Hoard extra Loot, for later use or pride*
		- *Visit shop to buy certain exclusive tools (not permanent to avoid power creep?)*
- Failing the requirement
	- Can still Exit but suffer from higher quota next round?
	- Player should always avoid this.

as long the round is finished successfully (enough Value), death penalty should not be too harsh.

up to debate: 
- should Exit also provide Radio infrastructure? let 'finished' player to help lost player?
- should Required Value be known from the beginning?
- Required Value scale with numbers of player?

### option 2: All Failed to leave
 - all progress in that round is lost. (some more punishment?)
 
### option 3?: Return to Entrance
need actual testing.
- Can return to Entrance as last resort / fail save option? (punishment for not even finding exist?)
- Player might abuse? discourage Progression? discourage heroic moments? erase tension?



Extra: There might be Artificial events during leave, to increase player stress (overkill pairing with Environmental hazard?)

 ---
# Main Events During Runs
There are different possible things to happen during runs.
Since Game Flow is directed by time, it should be somewhat **predictable** (phases?), even if it is randomized.
Thus, events are split into dependence with time:

### Time Independent / Time Weighted
- Creature encounter
	- Player might need/want to fight/avoid/hunt creatures.
- Radio Device Fixing
	- Radio Devices need some mini puzzles to bring back up. Should not be too hard.
	- May have some danger during fixing (attract creature/damage on fail etc), but should not be too annoying.

### Time Dependent
Generally, punish poor decision/planning/cooperation.
Intensity increase with phases? 

When time runs out, these events increase in odds (or just happens):
- Environmental Hazard
- Oppressive/Horror Creatures
  
Extra: To encourage risk play, some loot might spawn after time runs out:
- specific loot that is only available in threatening environment (storm in a glass?) 

---
# Extra

Pre-built locations:
- provide a specific aesthetic / story telling.