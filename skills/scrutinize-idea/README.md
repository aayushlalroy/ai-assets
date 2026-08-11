# Scrutinize Idea (`scrutinize-idea`)

> [!WARNING]
> **Pre-requisites**:
> - [`clarify-first`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/clarify-first/README.md) (Leaf Skill — gathers initial goals and boundaries)
> - [`evidence-ledger`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/evidence-ledger/README.md) (Leaf Skill — tracks unverified assumptions)
> - **Framework Spec**: Includes [`CRITIQUE.md`](CRITIQUE.md) (Steel-man, Pre-mortem, 5 Whys, RAT, ICE/RICE scoring)

---

## What This Skill Does
Red-teams and validates an idea in 1 pass using a structured critique framework (steel-man, pre-mortem, 5 Whys, RAT, ICE/RICE scoring) grounded in evidence, returning a structured critique, prioritized risk ledger, and refined version of the idea.

---

## When to Use

### Triggers & Scenarios
- **Single-Pass Red-Teaming**: When asked `"scrutinize this idea"`, `"red-team my idea"`, `"poke holes in an idea"`, or `"sanity-check an idea"`.
- **Pre-Mortem Analysis**: Uncovering load-bearing assumptions and potential failure modes before committing resources.

### When NOT to Use
- Do NOT use for multi-round worker/reviewer iterative review loops (use `adversarial-review-loop`).

---

## Examples

### Verdict & Risk Ledger Output
```markdown
| Value | Confidence | Risk | Verdict |
|-------|-----------|------|---------|
| high  | 40% (low)  | high | **REFINE** — validate assumptions before committing |

**Kill Criteria**: If permit processing exceeds 30 days, flip to NO-GO.
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/scrutinize-idea
```
