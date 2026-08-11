---
name: skill-metadata-optimizer
description: >-
  Generates, evaluates, and token-optimizes SKILL.md names and descriptions for maximum
  discoverability and minimum token cost. Trigger when drafting skill frontmatter, optimizing
  description tokens, or auditing skill names. Do NOT trigger for standard body logic editing.
disable-model-invocation: false
---

# Skill Metadata Optimizer

Reusable leaf primitive that generates, evaluates, and optimizes skill frontmatter (`name` and `description`). Ensures maximum discoverability when `disable-model-invocation: false` while keeping context token overhead strictly under ~50 words.

## Core Frontmatter Standards

### 1. Skill Name (`name`)
- Format: Lowercase kebab-case (`1-64` characters).
- Structure: Concise, descriptive verb-noun or noun phrase (e.g. `clarify-first`, `evidence-ledger`, `skill-creator`).

### 2. Skill Description (`description`)
- **Token Target**: `< 50 words` (~250 characters) to save context cost across prompts.
- **Three-Part Trigger Structure**:
  1. *Core Action*: What the skill does in 1 sentence.
  2. *User Prompt Triggers*: Explicit user phrases and intent (e.g. `"create skill"`, `"don't assume"`, `"gather requirements"`).
  3. *Workflow Event Triggers*: Runtime/context conditions (e.g. `mid-task ambiguity`, `missing key constraints`).
  4. *Negative Boundary*: 1 short sentence preventing false positives (`Do NOT trigger for...`).
- **Body Offloading Rule**: Remove UI/formatting templates, option lists, and caller skill lists from `description`. Verify these details live in the `SKILL.md` body.

## Optimization Workflow

When called with an existing `SKILL.md` file, raw frontmatter, or skill draft:

### Step 1: Metadata Audit
- Measure current `description` word count and estimated token cost.
- Inspect `SKILL.md` body to verify where execution details reside.
- Check trigger coverage: User Prompt triggers, Workflow Event triggers, and Negative boundaries.

### Step 2: Synthesis Engine
- Generate or refine `name`.
- Draft optimized `description` matching the Three-Part Trigger Structure (< 50 words).

### Step 3: Justification & Diff Report
Generate a transparent report for the user:
- **Original Description** vs **Proposed Description**
- **Token Impact**: Original word count ➔ New word count (% reduction).
- **Why the Change**: Exact details removed from frontmatter.
- **How Mitigated**: File pointers showing where those details live in the body.
- **Discoverability Analysis**: Trigger coverage breakdown (User prompt, Workflow, Negative boundary).

### Step 4: User Review Gate
Present the proposed metadata and report for user approval:
- If approved ➔ Apply frontmatter update.
- **If the user says NOT to change ➔ Respect decision and keep original intact.**
- If user requests tweaks ➔ Revise description accordingly.
