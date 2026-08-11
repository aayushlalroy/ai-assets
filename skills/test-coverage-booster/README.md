# Test Coverage Booster (`test-coverage-booster`)

> [!NOTE]
> **Pre-requisites**: None (Leaf Skill)

---

## What This Skill Does
Generates targeted unit and integration tests (JUnit 5 + Mockito by default) to cover new code branches and repair broken test suite assertions after code changes or rebases.

---

## When to Use

### Triggers & Scenarios
- **Post-Refactor Coverage**: Immediately after editing or refactoring a method, flow, or datatype.
- **Suite Fixes**: When tests fail after a rebase or signature change.
- **Coverage Asks**: `"boost test coverage"`, `"add unit tests"`, `"fix failing test suite"`.

### When NOT to Use
- Do NOT use for end-to-end UI browser automation or manual testing.

---

## Examples

### Generating JUnit 5 Tests for Boundary Conditions
```java
@Test
void calculateDiscount_shouldApplyMaxCap_whenTotalExceedsThreshold() {
    BigDecimal result = calculator.calculateDiscount(new BigDecimal("10000"));
    assertEquals(new BigDecimal("500"), result);
}
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/test-coverage-booster
```
