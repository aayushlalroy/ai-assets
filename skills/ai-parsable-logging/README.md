# AI-Parsable Logging (`ai-parsable-logging`)

> [!NOTE]
> **Pre-requisites**: None (Leaf Skill)

---

## What This Skill Does
Configures structured JSON logging with per-request correlation IDs (via MDC) and essential fields (`requestId`, `step`, `durationMs`). This allows automated tools, log aggregators, and AI agents to filter and trace requests across microservice hops using `jq` without fragile regex parsing.

---

## When to Use

### Triggers & Scenarios
- **Structured Logging Setup**: When asked `"add logging"`, `"improve logs"`, or `"make logs debuggable"`.
- **MDC & Correlation IDs**: Configuring per-request header propagation across microservices.
- **Log Aggregator Prep**: Preparing applications for automated jq or log-collector queries.

### When NOT to Use
- Do NOT use for simple log inspection or tailing existing log files.

---

## Examples

### Example Log Output & Querying
```json
{"timestamp":"2026-08-11T12:00:00Z","level":"ERROR","requestId":"req-abc123","step":"DB_QUERY","durationMs":1250,"message":"Connection timeout"}
```

```bash
# Querying errors via jq
cat app.log | jq 'select(.level=="ERROR")'
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/ai-parsable-logging
```
