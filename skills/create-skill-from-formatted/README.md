# Create Skill From Formatted (`create-skill-from-formatted`)

> [!NOTE]
> **Pre-requisites**:
> - [`skill-metadata-optimizer`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/skill-metadata-optimizer/README.md) (Leaf Skill — token-optimizes frontmatter description)

---

## What This Skill Does
Evaluates and optimizes existing or imported `SKILL.md` files for discoverability and token efficiency, auditing the body and delegating description optimization to `skill-metadata-optimizer`.

---

## When to Use

### Triggers & Scenarios
- **Importing Formatted Skills**: When given a pre-formatted `SKILL.md` file to evaluate.
- **Frontmatter Auditing**: Auditing skill discoverability and description token overhead.

### When NOT to Use
- Do NOT use for raw unformatted prompt ideas or conversation transcripts.

---

## Examples

### Input & Diff Report
```markdown
Parsing SKILL.md...
Delegating metadata audit to skill-metadata-optimizer...
Token Impact: 85 words ➔ 38 words (55% reduction).
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/create-skill-from-formatted
```
