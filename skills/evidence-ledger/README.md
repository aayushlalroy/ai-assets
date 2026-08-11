# Evidence Ledger (`evidence-ledger`)

> [!NOTE]
> **Pre-requisites**: None (Atomic Leaf Primitive Skill)

---

## What This Skill Does
`evidence-ledger` enforces strict factual discipline by requiring every load-bearing claim, decision, or recommendation to be explicitly tagged inline as either `[Evidenced: source]` or `[Assumption NN%: reasoning]`. It maintains an ordered Assumption Ledger table sorted by low-confidence + high-impact assumptions.

---

## When to Use

### Triggers & Scenarios
- **Factual Claims & Auditing**: When asked `"cite your sources"`, `"track assumptions"`, or `"how confident are you"`.
- **High-Stakes Architecture**: Making load-bearing technical decisions or cost/risk estimates.
- **Shared State in Loops**: Serving as shared memory across review rounds in adversarial loops.

### When NOT to Use
- Do NOT use for casual, low-stakes chat turns or simple syntax edits.

---

## Examples

### Example Inline Tags & Ledger
```markdown
We recommend using Postgres over DynamoDB [Evidenced: relational query patterns specified in PRD].

## Assumption Ledger
| # | Assumption | Strength | Raises ↑ / Lowers ↓ | Status |
|---|-----------|----------|---------------------|--------|
| 1 | Traffic < 1k QPS | 65% | ↑ user confirms · ↓ peak events implied | open |
| 2 | Budget ~$500 | 40% | ↑ user states figure · ↓ enterprise tier needed | open |
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/evidence-ledger
```
