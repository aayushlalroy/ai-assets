---
name: create-skill-from-prompt
description: >-
  Generates a new standalone leaf skill from a natural language prompt or idea. Trigger
  when creating skills from scratch, prompt specifications, or user instructions. Do NOT
  trigger when processing already formatted SKILL.md files.
disable-model-invocation: false
---

# Create Skill From Prompt

Converts raw user requirements or natural language prompt ideas into a fully formed, production-ready `SKILL.md` leaf skill directory inside `assets/skills/`.

## Execution Workflow

1. **Requirements Clarification**: Use [`clarify-first`](../clarify-first/SKILL.md) if scope, triggers, or execution boundaries are ambiguous.
2. **Draft SKILL.md Body**:
   - Write core rules, step-by-step instructions, templates, and examples.
   - Include `## When to use` and `## When NOT to use` sections.
3. **Metadata Generation (Delegated)**:
   Delegate name & description creation to [`skill-metadata-optimizer`](../skill-metadata-optimizer/SKILL.md):
   - Generates lowercase kebab-case `name`.
   - Generates token-optimized `< 50 word` `description` (User Prompt triggers + Workflow Event triggers + Negative boundary).
   - Sets `disable-model-invocation: false`.
4. **User Review Gate**: Present the drafted skill and metadata report to the user for approval before writing to `assets/skills/<skill-name>/SKILL.md`.
