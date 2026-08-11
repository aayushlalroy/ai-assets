# Skill Creator (`skill-creator`)

> [!WARNING]
> **Pre-requisites**:
> - [`create-skill-from-formatted`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/create-skill-from-formatted/README.md) (Sub-skill)
> - [`create-skill-from-prompt`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/create-skill-from-prompt/README.md) (Sub-skill)
> - [`create-skill-from-workflow`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/create-skill-from-workflow/README.md) (Sub-skill)
> - [`skill-metadata-optimizer`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/skill-metadata-optimizer/README.md) (Sub-skill)

---

## What This Skill Does
Orchestrates skill creation by detecting input type (formatted `SKILL.md`, raw prompt idea, or executed conversation workflow) and delegating to the appropriate specialized sub-skill before presenting an optimized diff report for mandatory human approval.

---

## When to Use

### Triggers & Scenarios
- **Master Entry Point**: When asked `"create a skill"`, `"build a new skill"`, or `"make a skill"`.

### When NOT to Use
- Do NOT use when updating an existing skill's execution body directly without frontmatter auditing.

---

## Examples

### Routing Logic
- Formatted file input ➔ `create-skill-from-formatted`
- Single prompt idea ➔ `create-skill-from-prompt`
- Chat transcript / session history ➔ `create-skill-from-workflow`

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/skill-creator
```
