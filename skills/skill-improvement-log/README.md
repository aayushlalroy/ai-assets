# Skill Improvement Log (`skill-improvement-log`)

> [!NOTE]
> **Pre-requisites**:
> - [`evidence-ledger`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/evidence-ledger/README.md) (Leaf Skill — used for root-cause claim tags)

---

## What This Skill Does
Appends proposed skill improvements to a persistent, human-reviewed backlog (`~/Development/cursor-knowledge-book/skill-improvement-backlog/`) when execution gaps or blind spots are identified. **It NEVER auto-edits skill files directly.**

---

## When to Use

### Triggers & Scenarios
- **Blind Spot Logging**: When asked `"log a skill improvement"`, `"record this blind spot"`, or `"add to the skill backlog"`.
- **Review Loop Misses**: Automatically invoked by the manager in `adversarial-review-loop` when confirming a valid-but-missed issue.

### When NOT to Use
- Do NOT use for automatic self-editing or self-applying modifications to skill files.

---

## Examples

### Entry Format
```markdown
### 2026-08-11 · Missed N+1 in Repository Query
- **skill:** scrutinize-idea
- **missed-issue:** Worker didn't check for nested entity fetch loops
- **status:** proposed
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/skill-improvement-log
```
