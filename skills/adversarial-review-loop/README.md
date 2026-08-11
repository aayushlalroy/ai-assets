# Adversarial Review Loop (`adversarial-review-loop`)

> [!WARNING]
> **Pre-requisites**:
> - [`clarify-first`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/clarify-first/README.md) (Leaf Skill — pins criteria before round 1)
> - [`evidence-ledger`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/evidence-ledger/README.md) (Leaf Skill — shared assumption state & tag format)
> - [`skill-improvement-log`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/skill-improvement-log/README.md) (Leaf Skill — logs persistent blind-spot backlog entries)
> - [`pr-review-principal`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/pr-review-principal/README.md) (Orchestrator — used when reviewing code artifacts)
> - **Prompt Library**: Includes [`prompts/PROMPTS.md`](prompts/PROMPTS.md) (Role templates for Worker, Reviewer, Manager)

---

## What This Skill Does
Runs a multi-round Worker/Reviewer/Manager adversarial review loop to harden any artifact. A fresh-eyes Reviewer (no prior context) inspects the artifact each round, the Worker evaluates each comment on merit (accept or push back), and the Manager logs in-loop blind spots and files persistent backlog proposals.

---

## When to Use

### Triggers & Scenarios
- **Multi-Round Hardening**: When asked `"run review loop"`, `"adversarial review"`, `"tear this apart"`, or `"review until solid"`.

### When NOT to Use
- Do NOT use for simple single-pass reviews.

---

## Examples

### In-Loop Blind-Spot Log
```markdown
## Blind-Spot Log
| # | Round | Blind spot (what worker missed) | Now checking for |
|---|-------|--------------------------------|------------------|
| 1 | 1 | Didn't verify festival dates | Always verify asserted dates against a source |
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/adversarial-review-loop
```
