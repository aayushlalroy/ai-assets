---
name: test-coverage-booster
description: >-
  Generates targeted unit and integration tests to cover new branches and repair broken assertions after code changes or rebases. Trigger on user prompt ("boost test coverage", "add unit tests", "fix failing test suite") or workflow events (post-refactor code diffs, broken test suites). Do NOT trigger for end-to-end UI browser automation.
disable-model-invocation: false
---

# Test Coverage Booster

The most-repeated task in my workflow: after any change, keep the suite green and
cover the new behavior.

## When to use
- Right after changing/refactoring a method, flow, or datatype.
- When tests fail after an edit or a rebase.
- When adding a new method/branch that needs coverage.

## Inputs
- `{changed_files}` — the files you touched (or "use git diff").
- `{failing_test_output}` — optional paste of the failing run.
- `{out_of_scope}` — anything not to touch.

## Steps
1. **Scope the change.** Read `git diff` to see exactly what behavior changed.
2. **Run the suite** and read failures from the root cause up.
3. **Repair broken tests:** update mock setups and assertions to the new
   signatures/return types. Do **not** weaken assertions to force green.
4. **Prune dead assertions:** remove tests only for behavior that was
   intentionally removed (e.g. a deleted patch path).
5. **Add coverage:** write a test for every new branch/edge (happy path, error
   path, boundaries, null/empty). Use Mockito for collaborators.
6. **Re-run until green.** Iterate.
7. **Report** the coverage delta and any gaps left (with reasons).

## Conventions
- JUnit 5 + Mockito; constructor injection makes mocking clean.
- One logical assertion focus per test; descriptive test names.
- Reproduce a bug with a failing test *before* fixing it.
- Respect `{out_of_scope}` strictly.

## Output
Green suite + new tests + a short note: "Covered X new branches; coverage now ~Y%;
untested: Z (reason)."
