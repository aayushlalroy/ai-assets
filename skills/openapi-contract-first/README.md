# OpenAPI Contract-First (`openapi-contract-first`)

> [!NOTE]
> **Pre-requisites**: None (Leaf Skill)  
> **Modes**: Includes [`schema-code-sync.md`](schema-code-sync.md) mode for reconciling spec drift against code.

---

## What This Skill Does
Designs REST APIs contract-first using OpenAPI 3.0 / 3.1 specifications under the root `api-spec/` directory structure (`schema/request/`, `schema/response/`, `schema/common/`, `examples/error/`, `examples/success/`, `common-components/`), bubbling out modular `$ref` JSON schemas with stringent validation constraints before DTO/code generation.

---

## Standard `api-spec/` Layout
```
api-spec/
├── openapi_consolidated.json            # Generated/compiled full OpenAPI spec
├── schema/
│   ├── openapi.json                     # Primary working spec (edited by developer)
│   ├── request/                         # Request payload JSON schemas
│   ├── response/                        # Response payload JSON schemas
│   └── common/                          # Repository-wide shared JSON schemas (entities)
├── examples/
│   ├── error/                           # JSON examples for error responses (RFC 7807)
│   └── success/                         # JSON examples for success responses
└── common-components/                   # Org-wide / RFC standard schemas (subtree/submodule or local)
```

---

## When to Use

### Triggers & Scenarios
- **REST API Design**: Designing or evolving REST endpoints contract-first using modular `$ref` JSON schemas.
- **Contract Drift**: Reconciling DTO code, serialization errors, or schema drift (`schema-code-sync` mode).
- **Prompts**: `"design REST API"`, `"create OpenAPI spec"`, `"contract-first API"`.

### When NOT to Use
- Do NOT use for GraphQL schemas, gRPC proto definitions, or DB migration scripts.

---

## Examples

### Modular `$ref` Schema Definition (`api-spec/schema/common/Share.json`)
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "required": ["id", "entity_id", "created_time"],
  "properties": {
    "id": { "type": "string", "format": "uuid" },
    "entity_id": { "type": "string", "minLength": 1, "maxLength": 64 },
    "created_time": { "type": "string", "format": "date-time" }
  }
}
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/openapi-contract-first
```
