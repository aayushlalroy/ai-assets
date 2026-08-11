# Request Layer Tracer (`request-layer-tracer`)

> [!NOTE]
> **Pre-requisites**:
> - [`ai-parsable-logging`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/ai-parsable-logging/README.md) (Leaf Skill — structured JSON logs with correlation IDs)
> - [`evidence-ledger`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/evidence-ledger/README.md) (Leaf Skill — records per-hop trace observations)

---

## What This Skill Does
Localizes failing API requests across architectural layers (Client → Gateway → Mesh Sidecar → App Pod → Database) by walking hop-by-hop logs with correlation IDs before diagnosing the root cause.

---

## When to Use

### Triggers & Scenarios
- **Multi-Hop Failures**: 504 Gateway Timeouts, 502 Bad Gateway, 503 Service Unavailable, or intermittent 500/403 errors across services.
- **Tracing Asks**: When asked `"trace where this request is failing"` or `"mesh vs app logs"`.

### When NOT to Use
- Do NOT use for Spring app startup errors or local unit test failures.

---

## Examples

### Diagnostic Trace Log Walkthrough
```
[Hop 1: Ingress Gateway] 200 OK (latency: 5020ms) -> [Hop 2: App Pod] 504 Gateway Timeout
-> Root Cause: App Pod blocked on downstream DB query timeout (5000ms threshold reached).
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/request-layer-tracer
```
