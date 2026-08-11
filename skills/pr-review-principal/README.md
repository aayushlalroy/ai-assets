# Principal-Engineer PR Review (`pr-review-principal`)

> [!WARNING]
> **Pre-requisites**:
> - [`openapi-contract-first`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/openapi-contract-first/README.md) (Leaf Skill — audits entity/schema agreement)
> - [`hibernate-nplus1-optimizer`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/hibernate-nplus1-optimizer/README.md) (Leaf Skill — audits persistence query patterns)
> - [`test-coverage-booster`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/test-coverage-booster/README.md) (Leaf Skill — evaluates branch test coverage)

---

## What This Skill Does
Applies a principal-engineer quality bar to code diffs and PRs, auditing contract-code consistency, edge cases, error contracts (`application/problem+json`), persistence performance (N+1 queries), security, and unit test coverage.

---

## When to Use

### Triggers & Scenarios
- **Pull Request Review**: Reviewing peer pull requests before merge.
- **Pre-Merge Self Audit**: Self-auditing code changes before pushing.
- **Adversarial Review Worker**: Acting as the code reviewer role within `adversarial-review-loop`.

### When NOT to Use
- Do NOT use for non-technical documentation or product ideas.

---

## Examples

### Prioritized Findings Output
```markdown
### Blocking
- `UserController.java:L45`: Missing `@Valid` on request payload; bypasses schema constraints.

### Should-fix
- `UserRepository.java:L82`: Unbounded query without pagination parameters.
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/pr-review-principal
```
