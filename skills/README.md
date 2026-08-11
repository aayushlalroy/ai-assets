# assets/skills/ — portable Agent Skills (source of truth)

The canonical, hand-authored `SKILL.md` agent skills distilled from the engineer's
real practice. Drop the folder into `~/.cursor/skills/` (or a project's
`.cursor/skills/`), or any `SKILL.md`-aware agent's skills path, and invoke a skill
by name. Cross-references between skills are **sibling-relative**, so the folder stays
portable wherever you copy it.

## Two families

- **Engineering runbooks** — `test-coverage-booster`, `openapi-contract-first`
  (+ its `schema-code-sync` mode), `pr-review-principal`, `jira-tech-story-drafter`,
  `spring-startup-doctor`, `request-layer-tracer`, `hibernate-nplus1-optimizer`,
  `git-recovery-runbook`, `bruno-request-generator`, `ai-parsable-logging`.
- **Idea-lab suite** — a composable set (`clarify-first`, `evidence-ledger`,
  `adversarial-review-loop`, `scrutinize-idea`, `visualize-idea-website`,
  `skill-improvement-log`, and the `idea-lab` orchestrator) for taking an idea from
  raw → critiqued → visualized.
- **Skill Creation suite** — a modular skill generation suite (`skill-creator` orchestrator,
  `create-skill-from-formatted`, `create-skill-from-prompt`, `create-skill-from-workflow`,
  and `skill-metadata-optimizer`) for parsing, token-optimizing, and distilling reusable skills.

Each subfolder is one skill (its `SKILL.md`, plus any prompt/reference files). The
catalog and rationale live in [`../../10-skills-from-prompts.md`](../../10-skills-from-prompts.md).

## How this differs from other skill folders

- **vs. top-level [`skills/`](../../skills/)** — that is a separate, self-contained
  **chat-mining refresh pipeline** (leaves → orchestrators → one meta-orchestrator)
  that *regenerates* insight documents. These `assets/skills/` are the engineer's
  **working skills** used while building software. No shared code; two of the pipeline
  skills merely *link back* to `evidence-ledger` / `skill-improvement-log` here to
  reuse those primitives.
- **vs. [`publishing/skills-pack/skills/`](../../publishing/skills-pack/skills/)** — that
  is an **intentional copy** of this folder, packaged with an MIT `LICENSE` + generated
  catalog for public release. This folder is the source of truth; the pack is the
  distributable rendering. Any public-only redaction is applied to the copy, not here.

## Duplicate notes

The duplication into `publishing/skills-pack/skills/` is deliberate (distribution
packaging). Improvement proposals for these skills are logged — never auto-applied —
into [`../../skill-improvement-backlog/`](../../skill-improvement-backlog/) by the
`skill-improvement-log` skill.
