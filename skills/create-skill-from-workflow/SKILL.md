---
name: create-skill-from-workflow
description: >-
  Distills a completed workflow, conversation log, or past execution history into a
  reusable leaf skill. Trigger when turning past workflows into skills or saying "make
  what we did a skill". Do NOT trigger for simple prompt ideas or importing formatted files.
disable-model-invocation: false
---

# Create Skill From Workflow

Distills past interactions, multi-step command logs, or conversation trajectories into a reusable, structured `SKILL.md` leaf skill inside `assets/skills/`.

## Execution Workflow

1. **Extract Workflow Trajectory**: Analyze recent conversation history, tool calls, or log steps.
2. **Synthesize Patterns**:
   - Generalize hardcoded values into variables/parameters.
   - Identify core decision rules, prerequisites, and failure recovery steps.
3. **Build SKILL.md Body**:
   - Create clear execution steps and verification checks.
4. **Metadata Generation (Delegated)**:
   Delegate name & description creation to [`skill-metadata-optimizer`](../skill-metadata-optimizer/SKILL.md):
   - Generates lowercase kebab-case `name`.
   - Generates token-optimized `< 50 word` `description` (User Prompt triggers + Workflow Event triggers + Negative boundary).
   - Sets `disable-model-invocation: false`.
5. **User Review Gate**: Present the distilled skill and metadata report to the user for approval before writing to `assets/skills/<skill-name>/SKILL.md`.
