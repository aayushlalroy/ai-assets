---
name: evidence-ledger
description: >-
  Tags claims/decisions as Evidenced or Assumption and maintains an assumption ledger table.
  Trigger on user prompt ("cite your sources", "track assumptions", "what's evidenced vs assumed",
  "how confident are you") or workflow events (making load-bearing factual claims/recommendations).
  Do NOT trigger for casual or trivial responses.
disable-model-invocation: false
---

# Evidence Ledger

Separate what you **know** from what you **assume**. Every load-bearing claim, decision,
or recommendation carries a tag so the user can audit your reasoning and target the
weak spots.

## The two tags (use these formats exactly)

Consistent formats matter — other skills parse and display these.

- **Evidenced** — backed by a source, observation, tool result, or the user's own words:

  `[Evidenced: <source or observation>]`

  e.g. `[Evidenced: user said budget is ₹50k]`,
  `[Evidenced: web — Gurudongmar permits require Indian ID, sikkimtourism.gov.in]`

- **Assumption** — anything not yet verified, with a confidence strength 0-100%:

  `[Assumption NN%: <why you believe it; what would raise/lower it>]`

  e.g. `[Assumption 65%: solo trip since no companions mentioned; ↑ if user confirms, ↓ if group implied]`

Strength guide: **90-100%** near-certain · **70-89%** likely · **40-69%** genuine toss-up
· **<40%** speculative. Never write 100% for something you didn't actually verify — that's
an Evidenced tag, not an assumption.

## The assumption ledger

Maintain a running table. Add a row whenever you make an assumption; update strength as
evidence arrives; mark rows resolved when verified or falsified.

```markdown
## Assumption Ledger
| # | Assumption | Strength | Raises ↑ / Lowers ↓ | Status |
|---|-----------|----------|---------------------|--------|
| 1 | Solo trip | 65% | ↑ user confirms · ↓ mentions companions | open |
| 2 | Budget ~₹50k | 40% | ↑ user states figure · ↓ names assets to buy | open |
| 3 | Festivals in Sept | 10% | verify calendar | ❌ falsified → Oct/Nov |
```

Order the ledger by risk: **low-strength + high-impact assumptions first** — those are
what to verify or ask about next.

## How to use it

1. As you produce claims/decisions, tag each inline with the format above.
2. Every `[Assumption …]` also gets a ledger row.
3. Prefer to **convert assumptions to evidence**: search the web, check a file, or ask
   the user (via [clarify-first](../clarify-first/SKILL.md)).
4. Keep an **evidence boundary**: never present an assumption as a fact. When strength is
   low and impact is high, flag it as a thing to resolve, not a conclusion.

## Lite mode

For small tasks, skip the full table and just tag inline. Keep the tags — they're cheap
and they keep you honest — but don't maintain a formal ledger for a one-off answer.

## Composition

- [clarify-first](../clarify-first/SKILL.md): unanswered questions become tagged
  assumptions here.
- [scrutinize-idea](../scrutinize-idea/SKILL.md): the risk/assumption list *is* this
  ledger, prioritized.
- [visualize-idea-website](../visualize-idea-website/SKILL.md): renders the ledger
  visually (assumption cards + confidence meters).
- [adversarial-review-loop](../adversarial-review-loop/SKILL.md): carries the ledger as
  shared state between rounds.
