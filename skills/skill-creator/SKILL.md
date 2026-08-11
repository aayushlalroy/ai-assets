---
name: skill-creator
description: >-
  Orchestrates creating and optimizing agent skills from formatted files, prompt
  ideas, or workflow logs. Trigger on "create skill", "import skill", "make a skill",
  or when converting inputs into reusable skills. Do NOT trigger for standard non-skill code edits.
disable-model-invocation: false
---

# Skill Creator Orchestrator

Master orchestrator for creating, importing, and optimizing agent skills. Automatically detects input formats and routes execution to specialized leaf sub-skills.

## Router Logic

Inspect the user's input and delegate to the appropriate leaf sub-skill:

1. **Formatted Skill File / String** (e.g. user passes an existing `SKILL.md`, a path to a skill file, or content exported from another resource):
   -> Delegate to [`create-skill-from-formatted`](../create-skill-from-formatted/SKILL.md)

2. **Natural Language Idea / Prompt** (e.g. user describes a task/behavior they want packaged into a skill):
   -> Delegate to [`create-skill-from-prompt`](../create-skill-from-prompt/SKILL.md)

3. **Workflow / Conversation Transcript / Logs** (e.g. distilling a recent execution or multi-step workflow into a skill):
   -> Delegate to [`create-skill-from-workflow`](../create-skill-from-workflow/SKILL.md)

## Composition & Primitive Tree

- **Master Orchestrator**: `skill-creator`
  - Leaf Primitive 1: [`create-skill-from-formatted`](../create-skill-from-formatted/SKILL.md)
  - Leaf Primitive 2: [`create-skill-from-prompt`](../create-skill-from-prompt/SKILL.md)
  - Leaf Primitive 3: [`create-skill-from-workflow`](../create-skill-from-workflow/SKILL.md)
  - Metadata Primitive: [`skill-metadata-optimizer`](../skill-metadata-optimizer/SKILL.md) (reusable frontmatter name/description generator & optimizer)
  - Helper Primitive: [`clarify-first`](../clarify-first/SKILL.md) (used for requirement clarification & review gates)
