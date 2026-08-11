---
name: jira-tech-story-drafter
description: >-
  Drafts technical user stories and design docs with acceptance criteria, technical approach, and test plans. Trigger on user prompt ("draft Jira story", "write design doc", "plan feature migration") or workflow events (pre-implementation technical planning). Do NOT trigger for non-technical product roadmaps or marketing writeups.
disable-model-invocation: true
---

# Jira Tech Story Drafter

Plan-first: capture the work as a clear story/design doc before writing code.

## When to use
- Breaking a feature/migration into a tracked story.
- Writing the plan doc that implementation will follow.

## Inputs
- `{work_summary}` — what needs to be built/changed.
- `{context}` — PRD, related tickets, current behavior.
- `{constraints}` — non-functionals, deadlines, dependencies.

## Structure to produce
1. **Title** — concise, action-oriented.
2. **Description / background** — the problem and why now.
3. **Acceptance criteria** — testable, bulleted, unambiguous.
4. **Technical approach** — API/contract changes, data model, affected
   services/layers, migration/sequencing if relevant.
5. **Out of scope** — explicit exclusions.
6. **Test plan** — unit/integration coverage expectations.
7. **Risks / rollout** — flags, backward compatibility, rollback.

## Conventions
- Keep it aligned to `{context}`; don't invent requirements.
- For large work, this doc is the frozen source of truth during implementation —
  don't edit it mid-build; track deviations separately.
- Prefer precise, checkable acceptance criteria over prose.

## Output
A ready-to-paste Jira story / design doc in Markdown.
