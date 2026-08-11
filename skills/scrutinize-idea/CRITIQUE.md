# Critique Framework

The red-team engine behind [scrutinize-idea](SKILL.md). Steel-man → attack with
evidence → refine. Every weakness carries a mitigation.

Search the web whenever a claim is externally checkable: dates, rules/permits, costs,
"has anyone actually done this", market/competitor existence. Cite what you find using
[evidence-ledger](../evidence-ledger/SKILL.md) tags.

---

## Part 1 — Lenses for common over-reach

Ideators tend to reason **solution-first and rationalize backward**, pivot fast, bundle
many goals into one fragile plan, under-specify budget/time, get attached to owned
assets, and make calendar/feasibility errors. These lenses target exactly that.

| Lens | Tell / trigger | Sharpest questions |
|------|----------------|--------------------|
| **Sunk-cost detector** | "otherwise there's no point", justifying by past spend | Would you choose this starting today with nothing invested? Is the prior commitment doing the reasoning? |
| **Timeline & dependency check** | dates asserted from memory, sequencing implied | Are these dates actually correct (verify)? What must happen before X? What breaks if one step slips? |
| **Feasibility & permissions gate** | merits debated before "can we even?" | Is it allowed/possible (permits, access, rules, budget ceiling, legality)? Who's done it, how? |
| **Scope-bundling splitter** | one plan carrying several unrelated goals | Which decisions are independent? If goal B fails, does A still stand? |
| **False-binary breaker** | "A vs B" either/or framing | What's the hybrid? Is there a third option that dominates both? |
| **Constraint surfacer** | no explicit budget/time/risk numbers | Hard budget, hard deadline, acceptable worst case — as numbers? |
| **Familiarity-vs-suitability** | "I know/own this so I'll use it" | Ignoring what you own, what's objectively best? How costly is switching, really? |
| **Adrenaline-vs-safety pre-mortem** | optimizing for excitement/tightness | What's the real limiter (weather, health, terrain, cash)? Find accounts of it going wrong. |

**Worked example (from a real trip-planning idea):** "I want to use my own bike,
otherwise there's no point in getting the bike" = sunk-cost + familiarity-vs-suitability.
The dominating third option (rent the purpose-built vehicle for the hard leg, keep the
owned one for the easy leg) beats the A-vs-B frame. The timeline lens caught a
"festivals are in September" error (actually Oct/Nov) that cascaded the entire plan into
the wrong season. The feasibility gate caught destinations that need permits rarely
granted to private vehicles. Lesson: verify dates and permissions **before** debating
the fun parts.

---

## Part 2 — General validation frameworks

### Pre-mortem
Imagine it's later and the idea failed spectacularly; work backward.
- *Top 3 ways it died? What early sign would we have seen? What would have prevented it?*

### First-principles thinking
Strip to fundamental truths, rebuild without inherited assumptions.
- *What's unarguably true? Which "requirements" are just convention? Rebuild from scratch — what stays?*

### Steel-man vs straw-man
Argue the strongest version before critiquing.
- *Most charitable, competent version? What would its smartest proponent say to my objection?*

### RAT — Riskiest Assumption Test
Find the assumption that, if wrong, kills the idea; test *that* first, cheaply.
- *What must be true for this to work? Which is most likely false AND most fatal? Cheapest test this week?*

### Lean Canvas / Business Model Canvas
For ventures/products: problem, segments, unique value prop, solution, channels,
revenue, cost, key metric, unfair advantage.
- *Who exactly has this problem? Why you? How does money/effort flow? The one metric that matters?*

### ICE scoring
Impact, Confidence, Ease, each 1-10. Two conventions:
- **Averaged (use for meters):** `ICE = (Impact + Confidence + Ease) / 3` → 0-10.
- **Multiplicative:** `ICE = Impact × Confidence × Ease` → 0-1000 (spreads scores wider).
Pick one, stay consistent. Default: averaged.

### RICE scoring
`RICE = (Reach × Impact × Confidence) / Effort`
- **Reach:** count affected per period.
- **Impact:** fixed scale — massive **3**, high **2**, medium **1**, low **0.5**, minimal **0.25**.
- **Confidence:** high **100%**, medium **80%**, low **50%**.
- **Effort:** person-months (the denominator).
Use RICE when reach/effort are estimable; ICE for quick gut-ranks.

### Wardley mapping
Map components on value chain (visible→invisible) vs evolution (genesis→commodity).
- *User need at the top? Which pieces are commodities you should never build? Where's the space heading?*

### Devil's advocate / red team
Explicit job of arguing against; separate person from position.
- *If paid to kill this, what's my strongest attack? What's everyone too polite to say?*

### 5 Whys
Ask "why" ~5 times to reach the root driver, not the symptom.
- *Why this? …and why does that matter? …until the real goal surfaces (often not the stated solution).*

### Inversion & second-order thinking
- **Inversion:** *What would guarantee failure? Are we doing any of it?*
- **Second-order:** *And then what? What does this cause 3 steps downstream?*

### MoSCoW & assumption mapping
- **MoSCoW:** Must / Should / Could / Won't — fights scope creep.
- **Assumption map:** plot on importance × evidence; top-right (important + unknown) = test first.

### Opportunity Solution Tree
outcome → opportunities (unmet needs) → solutions → experiments. Keeps solutions
tethered to a real outcome instead of solution-first drift.

---

## Part 3 — Combined scoring → verdict

Produce three reads: **Value** (ICE averaged 0-10, or RICE), **Confidence** (how much is
known vs assumed — driven by unverified load-bearing assumptions), **Risk** (likelihood
× impact of top failure modes). Then:

| Value | Confidence | Risk | Verdict |
|-------|-----------|------|---------|
| high | med–high | low–med | **GO** — proceed; test riskiest assumption first |
| high | low | any | **REFINE** — validate assumptions before committing |
| med | any | high | **REFINE** — reduce risk or shrink scope first |
| low | any | any | **NO-GO** — value doesn't justify it; say so plainly |

Always name **kill criteria**: the specific finding that would flip GO → NO-GO. If those
are untested, the honest verdict is REFINE, not GO.

---

## Part 4 — Practices worth borrowing

- **Source-linked claims** — every factual assertion links to its evidence.
- **Evidence boundary** — separate verified facts / user assumptions / your inferences.
- **Kill criteria up front** — state what would falsify the idea before evaluating.
- **Riskiest-assumption-first ordering** — order the critique by most-fatal × most-uncertain.
