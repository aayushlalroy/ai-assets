---
name: openapi-contract-first
description: >-
  Designs REST APIs contract-first using OpenAPI 3.0/3.1 specs in api-spec/ using modular $ref JSON schemas (request/response/common), stringent validation rules, RFC error examples, and common-components. Trigger on user prompt ("design REST API", "create OpenAPI spec", "contract-first API") or workflow events (evolving REST schemas). Do NOT trigger for GraphQL, gRPC, or DB migrations.
disable-model-invocation: false
---

# OpenAPI Contract-First

Design REST API contracts using OpenAPI 3.0 / 3.1 specifications before writing code, bubble out reusable JSON schemas with `$ref`, and enforce strict agreement across spec ⇄ entities ⇄ examples ⇄ generated DTOs.


## Contract consistency rule

*Canonical definition — other skills reference this instead of restating it.*

The request/response **entity/DTO**, the **OpenAPI schema**, the **examples**, and the **data model/table** must all agree on field **names**, **types**, **required/nullable**, and **formats**. The OpenAPI schema is the source of truth; code conforms to it. Any missing, extra, or mismatched field between these is a defect.

- To *design/evolve* an endpoint under this rule, follow the steps below.
- To *reconcile existing code* with the contract (serialization bugs, renames, drift), use the [schema-code-sync mode](schema-code-sync.md).

## Project Spec Layout (`api-spec/`)

Store all spec assets under the root `api-spec/` directory (or adapt inner folders if an existing repo uses a custom root spec folder):

```
api-spec/
├── openapi_consolidated.json            # Generated/compiled full OpenAPI spec (produced by build plugin)
├── schema/
│   ├── openapi.json                     # Primary working spec where paths & $refs are edited
│   ├── request/                         # JSON schemas for request payloads
│   ├── response/                        # JSON schemas for response payloads
│   └── common/                          # Repository-wide shared schemas (domain entities, sub-folders as needed)
├── examples/
│   ├── error/                           # JSON examples for error responses (RFC 7807 problem+json)
│   └── success/                         # JSON examples for success responses
└── common-components/                   # Org-wide / RFC standard schemas (subtree/submodule or local)
                                         # e.g., JSON Patch, offset pagination, problem details
```

## Schema Modularity & Validation Rules

1. **Modular `$ref` Reusability**: Whenever possible, bubble out reusable JSON schemas into standalone files under `schema/request/`, `schema/response/`, `schema/common/`, or `common-components/`. Reference them using `$ref` pointers (`$ref: '../schema/common/Share.json'`).
2. **Stringent Validation Constraints**: Never define loose, bare types (e.g. unconstrained `type: string`). Every primitive field MUST define stringent validation bounds:
   - **Strings**: `minLength`, `maxLength`, `pattern`, or `format` (`date-time`, `uuid`, `uri`, `email`).
   - **Numbers/Integers**: `minimum`, `maximum`, `format` (`int64`, `int32`, `float`, `double`).
   - **Enums**: Explicit `enum` allow-lists.
   - **Arrays**: `minItems`, `maxItems`, `uniqueItems: true` (when applicable).
3. **Error Standard**: All error responses MUST follow `application/problem+json` (RFC 7807) with examples in `examples/error/`.

## When to use
- Creating a new REST endpoint.
- Evolving an existing request/response shape.
- Reconciling generated code with a spec change.

## Inputs
- `{entities}` — domain objects involved.
- `{operation}` — method + path + purpose (e.g. `PATCH /v1/things/{id}`).
- `{style_guide}` — internal API standards (link/file), if any.

## Steps
1. **Establish folder structure**: Ensure `api-spec/` layout (`schema/request/`, `schema/response/`, `schema/common/`, `examples/error/`, `examples/success/`, `common-components/`) exists.
2. **Model modular schemas**: Create or update `$ref`'d JSON schema files in `schema/request/`, `schema/response/`, or `schema/common/` with stringent validation constraints.
3. **Update working spec**: Define operations in `schema/openapi.json`, referencing modular schemas via `$ref`.
4. **Add examples**: Store success JSON payloads in `examples/success/` and `application/problem+json` error payloads in `examples/error/`.
5. **Compile/Consolidate**: Run dependency plugins to generate `openapi_consolidated.json`.
6. **Lint & Version**: Lint spec against API guidelines; bump version tag (`/v1`, `/v2`) for breaking changes.
7. **Generate DTOs & Code**: Generate Java/TypeScript DTO classes from spec; implement Controller → Service → Repository.
8. **Verify**: Ensure code and tests strictly satisfy the OpenAPI contract consistency rule.

## Conventions
- The spec is the source of truth; code conforms to it, not vice versa.
- Partial updates (PATCH) validate an explicit allow-list of patch paths.
- Keep request/response schemas as separate `$ref'd` files under `api-spec/schema/`.

## Output
Updated `api-spec/` directory (modular schemas + spec + examples) + `openapi_consolidated.json` + generated DTOs & code + tests, all consistent.

