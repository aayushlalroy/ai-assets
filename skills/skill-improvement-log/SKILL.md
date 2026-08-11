---
name: skill-improvement-log
description: >-
  Appends proposed skill improvements to a human-reviewed backlog when identifying recurring execution gaps or blind spots. Trigger on user prompt ("log skill improvement", "record blind spot", "add to skill backlog") or workflow events (adversarial review manager logging missed issues). Do NOT trigger for automatic self-editing of skill files.
disable-model-invocation: true
---

# Skill Improvement Log

Capture "the worker should have caught this" misses into a **persistent, human-reviewed
backlog** so skills can be improved deliberately — never automatically.

## The one hard rule

**This skill never edits, enhances, or self-applies any skill.** It only **appends**
proposed improvements to backlog files. The user reviews them, marks each
accepted/rejected, and applies accepted ones by hand (or in a separate, explicit
request). If you ever feel tempted to "just fix the skill," stop — append a proposal
instead.

Why: auto-editing skills based on a single review miss causes silent drift, over-fitting
to one case, and unreviewable changes. A human gate keeps the skill library trustworthy.

## Backlog location & layout

`~/Development/cursor-knowledge-book/skill-improvement-backlog/`

- One markdown file per skill: `<skill-name>.md` (e.g. `scrutinize-idea.md`).
- `INDEX.md` — a roll-up table of every item across all skills with its status.
- `README.md` — the manual review workflow + entry format (read it if unsure).

Create `<skill-name>.md` on first use for that skill by copying the entry template below.

## Entry template

Append one block per miss to the relevant `<skill-name>.md`. Tag claims with
[evidence-ledger](../evidence-ledger/SKILL.md) format (`[Evidenced: …]` / `[Assumption NN%: …]`).

```markdown
### <YYYY-MM-DD> · <short title of the miss>
- **skill:** <skill-name>
- **round:** <review round # where it surfaced>
- **missed-issue:** <the valid issue the worker failed to catch>
- **root-cause:** <WHY the worker missed it — e.g. skill lacks a check for X> [Evidenced/Assumption tag]
- **suggested-enhancement:** <concrete change to the skill that would prevent recurrence>
- **severity:** low | medium | high
- **status:** proposed
```

`status` is the user-toggled field: `proposed` → `accepted` / `rejected` → `applied`.
Only the user changes it away from `proposed` (or when the user explicitly asks you to
mark something applied after they've applied it).

## Workflow

```
Improvement-Log Progress:
- [ ] Ensure backlog dir + INDEX.md + <skill-name>.md exist (create from template if not)
- [ ] Append the entry (status: proposed) to <skill-name>.md
- [ ] Add/refresh the matching row in INDEX.md
- [ ] Report what was logged; do NOT modify the target skill
```

1. **Locate/create** the backlog file for the skill.
2. **Append** the entry with `status: proposed`. Never rewrite existing entries.
3. **Update INDEX.md** — add a row (date, skill, title, severity, status) so pending
   items are visible in one place.
4. **Report** the logged proposal to the user and stop. The target skill is untouched.

### Manual review workflow (the user does this)

1. **AI proposes** — entries land as `status: proposed`.
2. **User reviews** each proposal in `<skill-name>.md`.
3. **User marks** `accepted` or `rejected` (and may edit the suggested enhancement).
4. **User applies** accepted items to the actual `SKILL.md` by hand — or later asks the
   AI, in an explicit separate request, to apply a specific accepted item — then sets
   `status: applied`.

The AI's job ends at step 1. It only advances status on explicit user instruction.

## Relationship to the blind-spot log

In [adversarial-review-loop](../adversarial-review-loop/SKILL.md) the **blind-spot log**
is the *in-loop, session* memory the worker self-checks against during the current run.
This backlog is the *cross-session, persistent* record for improving the skill later.
They are one pipeline, not two competing mechanisms: when the Manager confirms a
valid-but-missed issue, it (a) adds the in-loop blind-spot-log row **and** (b) invokes
this skill to append a `proposed` backlog entry. The blind-spot log fixes *this run*; the
backlog improves *the skill*.

## Composition

- Reuses [evidence-ledger](../evidence-ledger/SKILL.md) tag format for root-cause claims.
- Invoked by the Manager in [adversarial-review-loop](../adversarial-review-loop/SKILL.md).
