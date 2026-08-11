---
name: scrutinize-idea
description: >-
  Red-teams an idea using a structured critique framework (steel-man, pre-mortem, 5 Whys, ICE/RICE scoring) and returns a risk ledger. Trigger on user prompt ("scrutinize this idea", "red-team my idea", "poke holes in idea", "sanity check idea") or workflow events (initial idea validation). Do NOT trigger for multi-round adversarial review loops.
disable-model-invocation: true
---

# Scrutinize Idea

Turn a raw idea into a **refined, reality-checked** one. Be a constructive skeptic:
steel-man first, attack with evidence, then hand back mitigations and a better version.
Critique that only tears down is useless.

Full framework, lenses, and scoring: [CRITIQUE.md](CRITIQUE.md).

## Guiding stance

The user *wants* the bubble popped, but honestly — not cheerleading, not cynicism.
Ground critique in evidence; search the web when a claim is checkable (dates, rules,
costs, "has anyone actually done this"). Every weakness ships with a mitigation.

## Workflow

```
Scrutinize Progress:
- [ ] Clarify (clarify-first): pin the goal, constraints, success criteria
- [ ] Steel-man the idea (strongest version)
- [ ] Extract load-bearing assumptions (evidence-ledger tags)
- [ ] Run critique lenses → weaknesses + mitigations
- [ ] Pre-mortem with web evidence
- [ ] Score (ICE/RICE + risk/confidence) → GO / REFINE / NO-GO
- [ ] (Optional) adversarial-review-loop to harden the critique
- [ ] Output refined idea + prioritized ledger + open questions
```

1. **Clarify** — run [clarify-first](../clarify-first/SKILL.md) to get goal, budget,
   deadline, risk tolerance, and success criteria before critiquing.
2. **Steel-man** — state the strongest version in 2-3 lines so you attack the best case.
3. **Extract assumptions** — pull implicit beliefs into explicit, testable claims and
   tag each via [evidence-ledger](../evidence-ledger/SKILL.md).
4. **Run the lenses** — see below + CRITIQUE.md. Each hit → weakness + mitigation.
5. **Pre-mortem** — assume it failed; list causes; search the web for real accounts.
6. **Score** — ICE or RICE + risk/confidence → verdict.
7. **Harden (optional)** — for high-stakes ideas, run the critique through
   [adversarial-review-loop](../adversarial-review-loop/SKILL.md) so a fresh reviewer
   attacks the critique itself.

## Core critique lenses

Tuned to how ideators over-reach (questions + worked examples in CRITIQUE.md):

1. **Sunk-cost detector** — flags "otherwise there's no point" reasoning.
2. **Timeline & dependency check** — verify real dates, sequencing, prerequisites.
3. **Feasibility & permissions gate** — "Is this even allowed/possible?" before merits.
4. **Scope-bundling splitter** — separate independent goals fused into one fragile plan.
5. **False-binary breaker** — surface hybrids and a dominating third option.
6. **Constraint surfacer** — force budget, time, risk tolerance into numbers early.
7. **Familiarity-vs-suitability** — attachment to a known/owned thing over what fits.
8. **Adrenaline-vs-safety pre-mortem** — steel-man the exciting version, then find how
   it really fails.

Plus general frameworks (in CRITIQUE.md): first-principles, RAT, Lean Canvas, Wardley
mapping, devil's advocate, 5 Whys, inversion, second-order thinking, MoSCoW,
assumption mapping, opportunity solution tree.

## Output template

```markdown
## Steel-man
[Strongest version, 2-3 lines]

## Load-bearing assumptions (ledger)
| # | Assumption | Strength | ↑/↓ | Status |
...ordered low-strength + high-impact first...

## Critique (by lens)
- 🔴 [lens]: [weakness] [Evidenced/Assumption tag] → **Mitigation:** [fix]
- 🟡 [lens]: [concern] → **Mitigation:** [fix]

## Pre-mortem (top failure modes)
1. [how it fails] — likelihood × impact — [early warning sign] [evidence]

## Score
ICE/RICE: [numbers] | Risk: [low/med/high] | Confidence: [low/med/high]
**Verdict:** GO / REFINE / NO-GO — [one line] · **Kill criteria:** [what falsifies it]

## Refined idea
[Rewritten, tighter, reality-checked]

## Open questions (resolve before committing)
- [ ] ...
```

## Lite mode

Small/early idea: skip the review loop, ask only 1-3 clarifying questions, run the top
lenses, and give a short verdict + refined idea. Don't over-engineer a sanity check.

## Handoff

If the user wants to *see* the refined idea, hand off to
[visualize-idea-website](../visualize-idea-website/SKILL.md) — pass the refined idea and
the assumption ledger so risks are surfaced visually, not hidden behind pretty charts.
