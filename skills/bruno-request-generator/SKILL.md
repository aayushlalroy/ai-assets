---
name: bruno-request-generator
description: >-
  Generates ready-to-run curl commands and Bruno (.bru) API collection files from OpenAPI specs or endpoint code. Trigger on user prompt ("make Bruno collection", "give me curl for endpoints", "generate API requests") or workflow events (preparing endpoints for smoke testing). Do NOT trigger for Postman or Insomnia exports.
disable-model-invocation: true
---

# Bruno Request Generator

Turn an OpenAPI operation into a request you can run immediately — as `curl` or as a
Bruno `.bru` file.

## Inputs

- The OpenAPI spec (file or URL).
- Which operations (or "all").
- Base URL / environment (use a placeholder like `{{baseUrl}}` if unknown — ask via
  [clarify-first](../clarify-first/SKILL.md) if it matters).

## Steps

1. **Parse the operation(s):** method, path, path params, query params, required
   headers, `requestBody` schema, and security scheme (auth header).
2. **Build the body from the schema** using its `example`/`examples` if present, else
   synthesize a valid minimal body honoring `required`, types, `enum`, and formats.
3. **Emit the request** in the requested format(s) below.
4. **Parameterize** secrets/tokens and the base URL as variables — never inline a real
   credential.

## curl output

```bash
curl -X PATCH "{{baseUrl}}/v1/things/{id}" \
  -H "Authorization: Bearer {{token}}" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "example",
    "status": "ACTIVE"
  }'
```

Replace `{id}` with a real value; keep `{{baseUrl}}`/`{{token}}` as variables.

## Bruno (.bru) output

```
meta {
  name: Update Thing
  type: http
  seq: 1
}

patch {
  url: {{baseUrl}}/v1/things/:id
  body: json
  auth: bearer
}

params:path {
  id: 123
}

headers {
  Content-Type: application/json
}

auth:bearer {
  token: {{token}}
}

body:json {
  {
    "name": "example",
    "status": "ACTIVE"
  }
}
```

Put shared values (`baseUrl`, `token`) in a Bruno **environment**, not in each request.

## Workflow

```
Request Gen Progress:
- [ ] Read spec; select operations
- [ ] Extract method/path/params/headers/body-schema/security per operation
- [ ] Build valid bodies from schema examples (respect required/enum/format)
- [ ] Emit curl and/or .bru with variables for baseUrl + secrets
- [ ] Note any auth/env setup the user must do before running
```

## Notes

- If the spec has multiple servers, list them and let the user pick the environment.
- For arrays/nested objects, generate a minimal valid instance, not every optional
  field.
- Keep request/response field names exactly as the spec defines them.
