# Clarify First (`clarify-first`)

> [!NOTE]
> **Pre-requisites**: None (Atomic Leaf Primitive Skill)

---

## What This Skill Does
`clarify-first` forces the AI agent to stop and ask structured, multiple-choice questions before executing non-trivial or ambiguous requests. Every question features a `(Recommended)` choice with a brief justification, alternative options, and an explicit `Write your own` field.

---

## When to Use

### Triggers & Scenarios
- **Ambiguous Requests**: When a prompt has multiple reasonable technical or product interpretations.
- **Missing Constraints**: When critical details (budget, tech stack, target audience, deadline) are missing.
- **High-Impact Decisions**: Before taking actions that are costly or difficult to reverse.
- **Mid-Task Ambiguity**: When new forks or assumptions arise during multi-step execution.

### When NOT to Use
- Do NOT use for simple single-step fixes, trivial formatting, or fully specified requests.

---

## Examples

### Example 1: Clarifying Audience & Budget
```markdown
Before I build this dashboard, three quick questions:

**Q1: Who is the primary audience for this site?**
- a) Potential investors **(Recommended)** — your framing emphasized funding
- b) End users / customers
- c) Internal team / yourself
- d) Write your own: ______________________

**Q2: What's the hard budget ceiling?**
- a) Under $500 **(Recommended)** — matches early prototype stage
- b) $500–$2,000
- c) Write your own: ______________________
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/clarify-first
```
