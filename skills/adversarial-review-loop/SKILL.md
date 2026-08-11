---
name: adversarial-review-loop
description: >-
  Runs a multi-round Worker/Reviewer/Manager adversarial review loop that
  hardens any artifact: the Worker produces work, a Reviewer requests changes,
  the Worker critically accepts or pushes back on each comment with reasoning, a
  Manager logs blind spots the Worker should have caught, and a fresh
  no-context Reviewer takes the next round, repeating 3-4 rounds with clear
  stop conditions. Use when the user wants work rigorously reviewed, red-teamed,
  or "torn apart with fresh eyes", or says "run the review loop", "adversarial
  review", or "have it reviewed until solid". Composes clarify-first and
  evidence-ledger; used by scrutinize-idea and idea-lab.
disable-model-invocation: true
---

# Adversarial Review Loop

Harden an artifact through repeated adversarial review with **fresh eyes each round**
and a **manager that catches what the worker keeps missing**. The Worker is not a
pushover — it evaluates every comment on merit and pushes back on wrong ones.

Ready-to-paste role prompts: [prompts/PROMPTS.md](prompts/PROMPTS.md).

## Roles

| Role | Job |
|------|-----|
| **Worker** | Produces/revises the artifact. Critically evaluates each review comment: accept (fix) or reject (with reasoning). Not a pushover. |
| **Reviewer** | Reviews the current artifact and leaves specific, actionable comments requesting changes. A **fresh** reviewer (no prior context) is used each round. |
| **Manager** | Judges each *valid* comment: was it something the Worker should have caught? If yes, logs a **blind spot** (in-loop) the Worker must check for from now on, AND appends a persistent improvement proposal via [skill-improvement-log](../skill-improvement-log/SKILL.md). Also calls the stop condition. |

## Shared state (carried between rounds)

Persist these across rounds — they are the memory of the loop:

- **Artifact** — current version of the work.
- **Assumption ledger** — from [evidence-ledger](../evidence-ledger/SKILL.md).
- **Blind-spot log** — issues the Worker missed but should have caught; the Worker
  re-reads this before every revision and self-checks against it.
- **Comment disposition log** — each comment → accepted/rejected + reasoning (audit trail).

```markdown
## Blind-Spot Log
| # | Round | Blind spot (what worker missed) | Now checking for |
|---|-------|--------------------------------|------------------|
| 1 | 1 | Didn't verify festival dates | Always verify asserted dates against a source |
```

## The loop

```
Review Loop Progress:
- [ ] Round setup: clarify scope (clarify-first), init ledger + blind-spot log
- [ ] Round N: Worker produces/revises → Fresh Reviewer comments →
      Worker dispositions each (accept/reject + reason) → Manager logs blind spots
- [ ] Check stop conditions
- [ ] Finalize: summary of changes, remaining open assumptions, blind-spot log
```

**Each round:**
1. **Worker** produces v1 (round 1) or revises using the prior comments, the
   blind-spot log, and the ledger.
2. **Fresh Reviewer** (new subagent, no memory of past rounds — give it only the
   artifact + acceptance criteria) leaves comments.
3. **Worker** dispositions every comment: for each, *valid or not?* with reasoning.
   Fixes valid ones; pushes back (documented) on invalid ones.
4. **Manager** checks each comment the Worker accepted as valid: *should the Worker
   have caught this itself?* If yes → (a) add a new **blind-spot-log** row for this run,
   AND (b) invoke [skill-improvement-log](../skill-improvement-log/SKILL.md) to append a
   `proposed` entry to the persistent backlog (recording the missed issue, root cause,
   and a suggested skill enhancement). Manager then evaluates the stop conditions.

**Two logs, one pipeline (don't confuse them):**
- **Blind-spot log** = in-loop, this-session memory the Worker self-checks against each
  round (shown below).
- **Improvement backlog** = cross-session, persistent proposals for improving the *skill*
  itself, handled by [skill-improvement-log](../skill-improvement-log/SKILL.md). It is
  **never auto-applied** — the user reviews and applies accepted items by hand.

## Stop conditions

Stop when **either**:
- **Two consecutive rounds** produce no new *valid* issues (converged), or
- **4 rounds** reached (hard cap).

The Manager declares the stop. On stop, output: final artifact, summary of what changed,
the blind-spot log, and any still-open assumptions from the ledger.

## Running it with subagents

- Run each **fresh Reviewer** as a separate subagent so it genuinely has no prior
  context. Pass it ONLY: the current artifact + acceptance criteria + the review
  prompt. Do **not** pass it the blind-spot log or prior comments (that would
  contaminate the fresh eyes).
- The **Worker** and **Manager** retain full state across rounds (they *are* the memory).
- Copy the role prompts from [prompts/PROMPTS.md](prompts/PROMPTS.md).
- If subagents aren't available, simulate roles in sequence within one context, but
  explicitly "reset" when acting as the fresh Reviewer (ignore everything except the
  artifact + criteria).

## Lite mode (avoid over-engineering)

The full loop is expensive (latency + tokens + review fatigue). Scale it down:
- **Small/low-stakes artifact:** 1 round, single reviewer, no manager.
- **Medium:** 2 rounds.
- **High-stakes / user asked to "tear it apart":** full 3-4 rounds.
Always announce which mode you're running and why.

## Composition

- Uses [clarify-first](../clarify-first/SKILL.md) to pin acceptance criteria before
  round 1 (you can't review against unknown goals).
- Uses [evidence-ledger](../evidence-ledger/SKILL.md) for the shared assumption state
  and for reviewers to tag their claims.
- Uses [skill-improvement-log](../skill-improvement-log/SKILL.md) (Manager) to persist
  blind spots as human-reviewed skill-improvement proposals.
- For **code artifacts**, use [pr-review-principal](../pr-review-principal/SKILL.md) as
  the Reviewer role's checklist (contract/tests/security/conventions).
- Used by [scrutinize-idea](../scrutinize-idea/SKILL.md) and
  [idea-lab](../idea-lab/SKILL.md).
