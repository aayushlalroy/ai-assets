---
name: git-recovery-runbook
description: >-
  Maps git trouble scenarios to exact recovery commands (undo commits, recover bad rebase via reflog, resolve conflicts). Trigger on user prompt ("undo my last commit", "messed up rebase", "resolve conflicts", "recover lost commits") or workflow events (failed rebase/reset state). Do NOT trigger for routine git commit, push, or pull commands.
disable-model-invocation: true
---

# Git Recovery Runbook

Turn a git scare into the right command. **Always explain what a command does before
running it**, and **confirm before anything destructive** (`reset --hard`, force-push,
`clean -fd`).

## Safety first

- If work might be lost, **make a backup branch now**: `git branch backup/before-fix`.
- `git reflog` is your safety net — almost anything committed can be recovered from it.
- Never force-push a shared branch without confirming with the user (and never to
  `main`/`master`).

## Scenario → commands

### See what changed / where you are
```bash
git status                         # working tree + staged state
git log --oneline -10              # recent history
git diff --name-only origin/<branch>   # files differing from the remote
git diff origin/<branch>...HEAD    # your changes since diverging from remote
```

### Undo the last commit
```bash
git reset --soft HEAD~1     # undo commit, KEEP changes staged
git reset --mixed HEAD~1    # undo commit, keep changes unstaged (default)
git reset --hard HEAD~1     # DESTRUCTIVE: undo commit AND discard changes
```
If already pushed to your own (unshared) branch and you must rewrite:
```bash
git reset --soft HEAD~1 && git commit ...   # re-make the commit
git push --force-with-lease                 # safer than --force; confirm first
```

### Recover from a bad rebase / lost commits
```bash
git reflog                       # find the SHA from before things went wrong
git reset --hard <good-sha>      # restore to that state (backup branch first!)
```

### Undo a merge/rebase in progress
```bash
git rebase --abort     # bail out of an in-progress rebase
git merge --abort      # bail out of an in-progress merge
```

### Resolve conflicts across many files
```bash
git status                       # lists "both modified" files
# edit each, resolving <<<<<<< ======= >>>>>>> markers
git add <file>                   # mark resolved, one by one
git rebase --continue            # or: git merge --continue
git checkout --theirs <file>     # take the incoming version for a file
git checkout --ours <file>       # keep your version for a file
```

### Un-add / unstage
```bash
git restore --staged <file>      # unstage but keep changes
git restore <file>               # DESTRUCTIVE: discard working-tree changes to file
```

### Recover a deleted branch
```bash
git reflog                       # find the tip SHA of the deleted branch
git branch <name> <sha>          # recreate it
```

## Workflow

```
Git Recovery Progress:
- [ ] Clarify the goal + current state (git status / reflog)
- [ ] Make a backup branch if any loss is possible
- [ ] Explain the exact commands and their effect
- [ ] Run them (confirm before destructive/force operations)
- [ ] Verify with git status / git log
```

## Notes

- Use [clarify-first](../clarify-first/SKILL.md) to confirm intent when the ask is
  ambiguous ("undo" can mean unstage, uncommit, or discard — very different).
- `--force-with-lease` over `--force`: it refuses to overwrite others' new commits.
- When in doubt, prefer non-destructive options and reflog recovery over `--hard`.
