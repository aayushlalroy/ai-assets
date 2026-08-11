# Bruno Request Generator (`bruno-request-generator`)

> [!NOTE]
> **Pre-requisites**:
> - [`clarify-first`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/clarify-first/README.md) (Leaf Skill — confirms target environments and auth headers)

---

## What This Skill Does
Generates ready-to-run curl commands and Bruno (`.bru`) API collection files from OpenAPI specs or endpoint code with correct paths, parameter placeholders, headers, and valid JSON request bodies.

---

## When to Use

### Triggers & Scenarios
- **API Smoke Testing**: Creating Bruno CLI collections to test or smoke-test endpoints.
- **Request Generation**: When asked `"give me curl for these endpoints"` or `"make a Bruno collection"`.

### When NOT to Use
- Do NOT use for Postman or Insomnia export formats.

---

## Examples

### Generated Bruno `.bru` Request File
```hcl
meta {
  name: List Shares
  type: http
  seq: 1
}

get {
  url: {{baseUrl}}/v1/shares?entity_id=ent_123&page=0&page_size=20
  headers {
    Authorization: Bearer {{token}}
  }
}
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/bruno-request-generator
```
