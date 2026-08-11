---
name: ai-parsable-logging
description: >-
  Sets up structured JSON logging with correlation/trace IDs for machine-parsable tracing.
  Trigger on user prompt ("add logging", "improve logs", "make logs debuggable",
  "structured/JSON logging", "correlation id / MDC / request tracing") or workflow events
  preparing apps for automated log parsing. Do NOT trigger for reading or searching existing log files.
disable-model-invocation: false
---

# AI-Parsable Logging

Logs are easiest to debug — by a human *or* an agent — when they're **structured JSON
with a correlation id and per-request context**. Then "find all errors for request X"
is a one-line `jq`, not a regex guess.

> Key idea: JSON logs give **direct field access** — faster to filter, fewer tokens,
> no brittle parsing. Human-readable console locally; JSON in shared/prod environments.

## What to set up

1. **Structured JSON output.** Many modern frameworks support it natively; otherwise use
   a JSON encoder for your logging library. Example (Spring Boot 3.4+):

```yaml
logging:
  structured:
    format:
      console: logstash   # or ecs
```

For a human-readable local run, switch via profile (plain pattern locally, JSON
elsewhere).

2. **A correlation id per request** via MDC (Mapped Diagnostic Context), set in a filter
   at the edge of the app and cleared after:

```java
// pseudocode filter
String requestId = header("X-Request-Id", orElse(UUID.randomUUID().toString()));
MDC.put("requestId", requestId);
try { chain.doFilter(...); } finally { MDC.clear(); }
```

3. **High-value fields on every log event:**
   - `requestId` / `traceId` — group all logs of one request (and across services).
   - `step` — where in the flow this happened.
   - `level` — quick error filtering.
   - `durationMs` — spot slow operations.
   - relevant ids (userId/tenantId/etc.) — but **never secrets or PII** (mask/omit).

4. **Parameterized logging**, not string concatenation:

```java
log.info("share created for owner {} in {} ms", ownerId, durationMs);
```

## Reading the logs (human or agent)

```bash
cat app.log | jq 'select(.level=="ERROR")'                  # all errors
cat app.log | jq 'select(.requestId=="req-abc123")'         # one request, end-to-end
cat app.log | jq 'select(.durationMs > 1000)'               # slow operations
```

This is exactly what makes [request-layer-tracer](../request-layer-tracer/SKILL.md) fast:
one correlation id, followed across every hop.

## Workflow

```
Logging Setup Progress:
- [ ] Clarify: framework, versions, where logs are shipped (console/file/collector)
- [ ] Enable JSON output (native or encoder); keep plain console for local profile
- [ ] Add a request filter that sets/propagates a correlation id via MDC
- [ ] Add key fields (requestId, step, level, durationMs); mask secrets/PII
- [ ] Show the jq queries the team/agent will use to debug
```

## Cautions

- **Never log secrets, tokens, or PII.** Mask or omit; structured fields make accidental
  leaks easy to query — and easy to expose.
- Keep field names **consistent across services** so a trace id joins them.
- Propagate the correlation id on outbound calls (header) so downstream logs share it.
