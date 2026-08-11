---
name: pr-review-principal
description: Review a pull request (or your own diff before merge) with a principal-engineer lens — checking contract vs. entity vs. data-model consistency, tests/coverage, conventions, and security. Use before merging any backend change.
---

# Principal-Engineer PR Review

Raise the rigor bar: review like a principal engineer, focused on correctness,
consistency, and the contract.

## When to use
- Reviewing someone's PR.
- Self-reviewing your own change before opening/merging a PR.

## Inputs
- `{pr_or_diff}` — the PR URL or the diff.
- `{spec}` — the OpenAPI/GraphQL contract.
- `{entities}` — request/response entities and the data model/table.

## Review checklist
1. **Contract integrity:** apply the canonical
   [Contract consistency rule](../openapi-contract-first/SKILL.md#contract-consistency-rule)
   (entity/DTO ⇄ OpenAPI schema ⇄ examples ⇄ data model must agree on names, types,
   required/nullable, formats). Flag any missing/extra/mismatched field.
2. **Correctness:** logic, edge cases, null/empty handling, error paths.
3. **Error contract:** all errors use `application/problem+json`; correct status
   codes (mind 4xx vs. 5xx, and 502/503/504 semantics).
4. **Conventions:** constructor injection; Controller→Service→Repository layering;
   naming; no unrelated/out-of-scope changes.
5. **Persistence:** watch for N+1, missing projections, composite-key handling,
   migration/schema drift.
6. **Tests:** present, meaningful, and cover new branches; suite is green;
   coverage adequate.
7. **Security:** no hard-coded secrets; permission/ownership checks on mutations;
   dependency changes don't downgrade a security fix or conflict with the BOM.

## Output
A prioritized findings list: **Blocking → Should-fix → Nit**, each with the file/
line and a concrete suggestion. Lead with the highest-impact issue.

## Composition
This skill is the **Reviewer role for code artifacts** inside
[adversarial-review-loop](../adversarial-review-loop/SKILL.md): when that loop reviews a
PR or diff, each fresh Reviewer applies this checklist. The loop adds multi-round fresh
eyes, worker push-back, and blind-spot tracking around this review.
