# Jira Tech Story Drafter (`jira-tech-story-drafter`)

> [!NOTE]
> **Pre-requisites**: None (Leaf Skill)

---

## What This Skill Does
Drafts plan-first technical user stories and design specifications in Markdown format, complete with Description, Acceptance Criteria, Technical Approach, Out-of-Scope boundaries, and Test Plans.

---

## When to Use

### Triggers & Scenarios
- **Technical Planning**: Breaking a feature or migration into a tracked story before coding.
- **Design Specifications**: Drafting design docs or Jira engineering tickets.
- **Prompts**: `"draft Jira story"`, `"write design doc"`, `"plan feature migration"`.

### When NOT to Use
- Do NOT use for marketing copy, product roadmaps, or non-technical writeups.

---

## Examples

### Tech Story Layout
```markdown
## Description
Migrate authentication from session cookies to JWT tokens.

## Acceptance Criteria
- [ ] Issued JWTs carry 15-minute expiration.
- [ ] Refresh token endpoint validates revoked claims.

## Technical Approach
Implement JJWT filter in Spring Security pipeline.
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/jira-tech-story-drafter
```
