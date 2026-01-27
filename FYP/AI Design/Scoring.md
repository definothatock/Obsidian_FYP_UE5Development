
---

## 1. Guiding Principles

1. **Separation of concerns**
    
    - **Per-entry facts** (memory array) should stay subject-centric: perception signals, relationship context, recency, etc.
    - **Global state** (per creature) should capture mood, needs, and personality trends.
2. **Score purpose clarity**
    
    - A score should exist only if it (a) resolves a decision tradeoff or (b) feeds directly into a downstream system (motivation selection, targeting, tactical mode).
    - Each score ought to map to observable behavior (“This rises → AI more likely to do X”).
3. **Layered evaluation cadence**
    
    - **Event-driven pulses** update raw perception facets immediately.
    - **Timer-driven passes** (e.g., every 1–3s) recompute derived scores, aggregate global motivations, and perform target arbitration.
    - Personality/long-term mood updates can run even slower (seconds to minutes) if/when introduced.

---

