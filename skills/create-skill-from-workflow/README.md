# Create Skill From Workflow (`create-skill-from-workflow`)

> [!NOTE]
> **Pre-requisites**:
> - [`skill-metadata-optimizer`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/skill-metadata-optimizer/README.md) (Leaf Skill — token-optimizes frontmatter description)

---

## What This Skill Does
Distills an executed conversation trajectory, multi-step workflow transcript, or successful problem-solving session into a reusable, production-ready `SKILL.md` file.

---

## When to Use

### Triggers & Scenarios
- **Workflow Distillation**: When asked `"turn what we just did into a skill"`, `"make a skill from this session"`, or `"package this workflow"`.

### When NOT to Use
- Do NOT use for raw single-line prompt snippets.

---

## Examples

### Distillation Output
Input: A 12-turn debugging session fixing a memory leak in a Node.js microservice.  
Output: Synthesized `node-memory-leak-debugger/SKILL.md` skill with reproducible steps.

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/create-skill-from-workflow
```
