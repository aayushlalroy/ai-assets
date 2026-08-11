# Standalone Prompts

Copy-pasteable prompt templates. Replace `<…>` placeholders. Tags follow
[evidence-ledger](../../evidence-ledger/SKILL.md): `[Evidenced: <source>]` and
`[Assumption NN%: <why>]`.

---

## Clarifying-questions prompt

```
Before producing anything, identify what is ambiguous or under-specified about the
task below. Ask me the highest-impact questions (numbered). For EACH question give:
- a) a Recommended option marked "(Recommended)" with a one-line why
- b) 2-4 other viable options
- c) "Write your own: ____"
Do not assume — ask first. Batch all questions in one message, ordered by impact.

TASK: <describe the task / idea>
```

---

## Evidence-tagging prompt

```
Rewrite the following so that EVERY load-bearing claim or decision is tagged:
- [Evidenced: <source/observation>] when backed by a source, tool result, or my words
- [Assumption NN%: <why; what would raise/lower confidence>] otherwise
Then append an "Assumption Ledger" table (#, assumption, strength, ↑/↓, status),
ordered by low-strength + high-impact first. Never present an assumption as fact.

CONTENT: <paste content>
```

---

## Worker prompt (round 1 — produce)

```
You are the WORKER. Produce <artifact> meeting the acceptance criteria below.
Tag claims/decisions as [Evidenced: …] or [Assumption NN%: …] and keep an assumption
ledger. Aim for genuinely defensible work — a tough reviewer will attack it next.

ACCEPTANCE CRITERIA:
<bullet list of what "good" means>

CONTEXT/INPUT:
<the idea, refined idea, requirements, ledger so far>
```

---

## Worker prompt (later rounds — revise + disposition)

```
You are the WORKER revising your artifact. You are NOT a pushover: evaluate each
review comment on its merits.

For EACH comment, output:
- Comment: <quote>
- Verdict: VALID or INVALID
- Reasoning: <why — cite evidence or logic>
- Action: <fix made> OR <why you're pushing back>

Before revising, re-read the BLIND-SPOT LOG and self-check the artifact against every
entry. Update the assumption ledger. Then produce the revised artifact.

CURRENT ARTIFACT:
<paste>
REVIEW COMMENTS:
<paste reviewer comments>
BLIND-SPOT LOG:
<paste>
ASSUMPTION LEDGER:
<paste>
```

---

## Fresh-reviewer prompt (no prior context — use each round)

```
You are a REVIEWER seeing this artifact for the FIRST time. You have no history and
no stake in it. Review it hard against the acceptance criteria and leave specific,
actionable comments requesting changes. For each comment:
- Location/quote
- Problem (be concrete)
- Suggested change
- [Evidenced: …] or [Assumption NN%: …] for any factual claim you make
Prioritize the most damaging issues first. Do not rubber-stamp; find the real weaknesses.

ARTIFACT:
<paste ONLY the artifact>
ACCEPTANCE CRITERIA:
<paste criteria — nothing else>
```

> Give the fresh reviewer ONLY the artifact + criteria. Do not paste the blind-spot log
> or prior rounds — that would destroy the fresh-eyes property.

---

## Manager prompt

```
You are the MANAGER. For each review comment the Worker accepted as VALID, judge:
"Should the Worker have caught this itself, given the task and prior rounds?"
- If YES: (a) add a BLIND-SPOT LOG row — describe the miss and the general check the
  Worker must run every future round to prevent its recurrence; AND (b) invoke the
  skill-improvement-log skill to APPEND a `proposed` entry to the persistent backlog at
  ~/Development/cursor-knowledge-book/skill-improvement-backlog/<skill>.md
  (date, skill, round, missed-issue, root-cause, suggested-enhancement, severity,
  status: proposed) and refresh INDEX.md. NEVER edit or auto-apply the target skill —
  only append a proposal for the user to review.
- If NO (genuinely needed fresh eyes): note it, no blind spot, no backlog entry.

Then decide the STOP CONDITION:
- Stop if the last TWO rounds produced no new valid issues, OR this was round 4.
- Otherwise, continue to the next round with a fresh reviewer.
Output: updated blind-spot log, stop/continue decision + reason, and (if stopping) a
final summary of changes and remaining open assumptions.

VALID COMMENTS THIS ROUND:
<paste>
BLIND-SPOT LOG:
<paste>
ROUND NUMBER: <n>
ISSUES-FOUND HISTORY: <e.g. R1:6, R2:2, R3:0>
```
