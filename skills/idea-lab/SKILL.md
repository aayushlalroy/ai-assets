---
name: idea-lab
description: >-
  Orchestrates the end-to-end idea workflow — clarify, scrutinize (with the
  adversarial review loop), refine, then visualize as an interactive website —
  by delegating to the small composable skills rather than duplicating them. Use
  when the user wants the full treatment on an idea: "run my idea through the
  lab", "scrutinize and then visualize this idea", "refine and build a site for
  my idea", or when they have an idea and want it both pressure-tested and made
  visible. Composes clarify-first, evidence-ledger, scrutinize-idea,
  adversarial-review-loop, and visualize-idea-website.
disable-model-invocation: true
---

# Idea Lab

Top-level orchestrator: **clarify → scrutinize → refine → visualize**. It coordinates
the small skills; it does not re-implement them. Read the delegated skill when you
enter its phase.

Full docs, usage/when-to-use, and the composition graph: [README.md](README.md).

## The pipeline

```
Idea Lab Progress:
- [ ] Phase 0: Clarify + choose mode (lite / standard / deep)
- [ ] Phase 1: Scrutinize → refined idea + prioritized assumption ledger
- [ ] Phase 2: (deep only) Harden the critique via the review loop
- [ ] Decision point: verdict → stop, or continue to visualize
- [ ] Phase 3: Visualize the refined idea as an interactive website
- [ ] Wrap-up: recap verdict, open questions, how to run the site
```

### Phase 0 — Clarify + pick mode
Run [clarify-first](../clarify-first/SKILL.md) to pin goal, constraints, success
criteria, and what the user wants (critique only vs full site). Choose a mode:

| Mode | When | Loop rounds | Visualize? |
|------|------|-------------|-----------|
| **Lite** | small/early idea, quick gut-check | 0 (skip loop) | usually no |
| **Standard** | real decision, moderate stakes | 1-2 | optional |
| **Deep** | high stakes / "tear it apart" | 3-4 | yes |

Announce the chosen mode and why.

### Phase 1 — Scrutinize
Delegate to [scrutinize-idea](../scrutinize-idea/SKILL.md). Output: structured critique,
prioritized risks/assumptions with strengths (the [evidence-ledger](../evidence-ledger/SKILL.md)),
and a refined idea.

### Phase 2 — Harden (deep mode only)
Run the critique + refined idea through
[adversarial-review-loop](../adversarial-review-loop/SKILL.md) so fresh reviewers attack
it across 3-4 rounds and the manager logs blind spots. Carry the ledger + blind-spot log
as shared state.

### Decision point
Present the verdict (GO / REFINE / NO-GO), refined idea, and open questions.
- **NO-GO:** stop; don't build a site for a dead idea unless the user still wants it to
  think through.
- **GO / REFINE + user wants it:** continue with the **refined** idea.

### Phase 3 — Visualize
Delegate to [visualize-idea-website](../visualize-idea-website/SKILL.md), passing the
refined idea and the ledger. The Assumptions & Risks module must surface the ledger so
the site stays honest.

### Wrap-up
Recap verdict, unresolved assumptions, and how to run the site (route-by-route tour).

## State carried across phases

One shared **assumption ledger** and (deep mode) **blind-spot log** flow through every
phase. Don't restart them per skill — pass them along so the site visualizes the same
assumptions the critique produced.

## Shortcomings + mitigations (be honest)

- **Loop latency/cost** → mode tiers; lite skips the loop; hard 4-round cap + converge stop.
- **Over-engineering small ideas** → lite mode default for low stakes; visualize is opt-in.
- **Review fatigue / diminishing returns** → stop after two no-new-issue rounds.
- **Fresh-reviewer setup overhead** → prompts pre-written in
  [adversarial-review-loop/prompts/PROMPTS.md](../adversarial-review-loop/prompts/PROMPTS.md).
- **Pretty visuals mask weak logic** → scrutinize gates visualize; ledger surfaced in the UI.

## Composition

Delegates to (never duplicates): [clarify-first](../clarify-first/SKILL.md),
[evidence-ledger](../evidence-ledger/SKILL.md),
[scrutinize-idea](../scrutinize-idea/SKILL.md),
[adversarial-review-loop](../adversarial-review-loop/SKILL.md),
[visualize-idea-website](../visualize-idea-website/SKILL.md).
