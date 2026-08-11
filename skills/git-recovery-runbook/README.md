# Git Recovery Runbook (`git-recovery-runbook`)

> [!NOTE]
> **Pre-requisites**:
> - [`clarify-first`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/clarify-first/README.md) (Leaf Skill — used to confirm recovery target before running destructive resets)

---

## What This Skill Does
Maps common Git emergency scenarios (lost commits, dropped branches, corrupted rebases, merge conflicts) to exact recovery commands using `git reflog`, safety branches, and non-destructive resets.

---

## When to Use

### Triggers & Scenarios
- **Git Disasters**: When asked `"undo my last commit"`, `"messed up rebase"`, `"resolve conflicts"`, or `"recover lost commits"`.
- **Reflog Recovery**: Recovering commits or branches dropped after `git reset --hard`.

### When NOT to Use
- Do NOT use for routine commit, push, or pull commands.

---

## Examples

### Reflog Recovery Command Sequence
```bash
# 1. Create a safety branch
git branch safety-backup-HEAD

# 2. Inspect reflog to find dropped commit hash
git reflog

# 3. Restore branch to target hash
git reset --hard HEAD@{2}
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/git-recovery-runbook
```
