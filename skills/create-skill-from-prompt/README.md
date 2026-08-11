# Create Skill From Prompt (`create-skill-from-prompt`)

> [!NOTE]
> **Pre-requisites**:
> - [`skill-metadata-optimizer`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/create-skill-from-prompt/README.md) (Leaf Skill — token-optimizes frontmatter description)

---

## What This Skill Does
Transforms a raw prompt idea or text prompt into a fully formatted `SKILL.md` spec file with structured sections (`# Title`, `## Core rule`, `## When to use`, `## Steps`, `## Composition`).

---

## When to Use

### Triggers & Scenarios
- **Prompt to Skill**: When asked `"turn this prompt into a skill"` or `"make a skill from this prompt idea"`.

### When NOT to Use
- Do NOT use when given an already formatted `SKILL.md` file (use `create-skill-from-formatted`).

---

## Examples

### Usage Scenario
Input: *"I want a skill that checks Java records for proper validation annotations."*  
Output: Formatted `SKILL.md` spec created under target directory.

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/create-skill-from-prompt
```
