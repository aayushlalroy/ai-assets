---
name: clarify-first
description: >-
  Asks structured clarifying questions instead of assuming. Trigger on user prompt
  (ambiguous/under-specified requests, "clarify first", "don't assume", "ask questions",
  "gather requirements") or workflow events (mid-task ambiguity, missing key constraints,
  non-trivial execution forks). Do NOT trigger for trivial/routine tasks or fully specified asks.
disable-model-invocation: true
---

# Clarify First

Never assume. When anything is ambiguous or under-specified, **ask before you act**.
Every ambiguity resolved up front saves a wrong deliverable later.

## Core rule

Before starting a non-trivial task, surface the open questions and ask them. Do not
silently pick an interpretation. If you *must* proceed (user unavailable), state your
assumptions explicitly and tag them with [evidence-ledger](../evidence-ledger/SKILL.md)
so they're visible and revisable.

## When to ask

- The request has more than one reasonable interpretation.
- A key constraint is missing: scope, budget, deadline, audience, tech, success criteria.
- A default choice would be hard/expensive to reverse later.
- **New ambiguity appears mid-task** — re-ask; don't push through on a guess.

## The question format (always this shape)

Every question offers three kinds of answers:

- **(a) A Recommended option**, marked `(Recommended)`, with a one-line why.
- **(b) Other viable options** you actually considered (2-4 of them).
- **(c) An explicit freeform option**: "Write your own."

Template:

```markdown
**Q1: <the question — one sentence>**
- a) <option> **(Recommended)** — <why this is the default>
- b) <alternative option>
- c) <another alternative>
- d) Write your own: ______________________
```

## Batching

Ask all currently-known questions **in one batch** (numbered Q1, Q2, …), not one at a
time. Order by impact — the answer that most changes the plan goes first. Keep it to
the questions that actually change what you'd build; don't pad.

If the user answers only some, proceed on those and re-ask the rest. When their answers
reveal new forks, run another (smaller) batch.

## Lite mode

For small/low-stakes tasks, ask **only the 1-3 highest-impact questions**, or state a
single clearly-labeled assumption and invite correction. Don't interrogate the user
over a trivial ask — that's its own failure mode.

## Example

```markdown
Before I build this, three quick questions:

**Q1: Who is the primary audience for this site?**
- a) Potential investors **(Recommended)** — your framing emphasized funding
- b) End users / customers
- c) Internal team / yourself
- d) Write your own: ______________________

**Q2: What's the hard budget ceiling?**
- a) Under ₹50k **(Recommended)** — matches a solo/early stage
- b) ₹50k–₹2L
- c) No fixed ceiling yet
- d) Write your own: ______________________

**Q3: Deadline?**
- a) No fixed date, quality first **(Recommended)**
- b) Within 2 weeks
- c) Write your own: ______________________
```

## Composition

- Pairs with [evidence-ledger](../evidence-ledger/SKILL.md): any question you *don't*
  get answered becomes a tagged `[Assumption NN%]`.
- Called first by [scrutinize-idea](../scrutinize-idea/SKILL.md),
  [visualize-idea-website](../visualize-idea-website/SKILL.md), and
  [idea-lab](../idea-lab/SKILL.md).
