# Mode: schema-code-sync

A mode of [openapi-contract-first](SKILL.md) for the **reverse/maintenance** direction:
an existing contract or generated code changed, and now the entities, DTOs, generated
classes, and (de)serialization must be brought back into agreement. Use this when
diagnosing serialization bugs or propagating a schema/field change through existing
code, rather than designing a brand-new endpoint.

## When to use this mode

- A response field is missing/null, or you get a (de)serialization mismatch
  (e.g. `MismatchedInputException`, unexpected JSON shape).
- A field was renamed or retyped in the spec and code/tests must follow.
- Generated classes drifted from the spec after a change.

## The consistency target

Keep all four in agreement (the canonical rule lives in
[SKILL.md → Contract consistency rule](SKILL.md#contract-consistency-rule)):

```
OpenAPI schema  ⇄  entity/DTO  ⇄  examples  ⇄  generated classes / data model
```

## Folder Structure Reference

Reconciliation happens against the canonical `api-spec/` directory:
- `api-spec/schema/openapi.json` (working spec)
- `api-spec/openapi_consolidated.json` (compiled spec)
- `api-spec/schema/request/`, `api-spec/schema/response/`, `api-spec/schema/common/` (modular `$ref` schemas)
- `api-spec/common-components/` (RFC standard schemas)
- `api-spec/examples/error/`, `api-spec/examples/success/` (JSON payload examples)

## Steps

1. **Locate the source of truth.** The OpenAPI schemas under `api-spec/schema/` are canonical. Read the operation's request/response schemas and examples.
2. **Diff against code.** Compare field **names**, **types**, **required/nullable**, and stringent **formats/constraints** (`minLength`, `maxLength`, `pattern`, `minimum`, `maximum`) between the modular schemas and the entity/DTO/generated class.
3. **Find the drift.** Common causes: a rename not propagated; a projection/DTO not mapping a column to the response field; missing getter/annotation; type/constraint mismatch.
4. **Fix toward the contract.** Update the code (or projection mapping) to match the schema — not the other way around, unless the contract itself is wrong (then evolve the spec deliberately under `api-spec/schema/` and re-consolidate).
5. **Propagate everywhere.** Apply the rename/type change across all usages **and tests** (a partial refactor causes `cannot find symbol` build failures).
6. **Add (de)serialization tests** asserting the exact JSON shape and constraint validation so the drift can't silently return.

## Serialization checklist

- Field names match the schema exactly (respect any documented naming, e.g. `created_on` vs `creationTime`) — apply the rename consistently.
- Stringent types/formats line up (e.g. `integer/int64` ↔ `Long`; `date-time` ↔ `OffsetDateTime`/`Instant`; validation regexes match).
- `required` fields are non-null in code; nullable fields tolerate absence.
- Projections select and alias columns to the exact response field names.
- Examples in `api-spec/examples/` are still valid after the change.

## Output

Code + tests consistent with `api-spec/`, the specific drift explained, and a serialization test guarding the shape.
