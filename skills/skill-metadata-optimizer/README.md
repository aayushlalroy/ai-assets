# Skill Metadata Optimizer (`skill-metadata-optimizer`)

> [!NOTE]
> **Pre-requisites**: None (Leaf Meta-Skill)

---

## What This Skill Does
Evaluates, token-optimizes, and structures `SKILL.md` frontmatter (`name` and `description`) for maximum LLM discoverability and minimum token cost across prompt turns (< 50 words target).

---

## When to Use

### Triggers & Scenarios
- **Frontmatter Optimization**: When asked `"optimize skill description"`, `"fix frontmatter"`, or `"audit skill metadata"`.
- **Delegated Audit**: Called by `create-skill-from-*` skills to format descriptions.

### When NOT to Use
- Do NOT use for standard markdown body logic editing.

---

## Examples

### Three-Part Description Format
1. Core Action (1 sentence)
2. User Prompt Triggers (`"create skill"`, `"optimize frontmatter"`)
3. Workflow Event Triggers (`mid-task ambiguity`)
4. Negative Boundary (`Do NOT trigger for...`)

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/skill-metadata-optimizer
```
