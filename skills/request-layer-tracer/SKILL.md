---
name: request-layer-tracer
description: >-
  Localizes failing API requests across architectural layers (client -> gateway -> service mesh -> app -> DB) by correlating hop logs. Trigger on user prompt ("trace where request is failing", "mesh vs app logs", "504 gateway timeout") or workflow events (multi-hop service timeouts, intermittent 5xx). Do NOT trigger for Spring app startup errors.
disable-model-invocation: true
---

# Request Layer Tracer

Find **where** a request breaks before asking **why**. Chasing the "why" in the wrong
layer wastes the most time. Localize the hop first, then debug that hop.

## The layer model

```
client → edge/gateway → service mesh sidecar (e.g. Istio/Envoy) → app pod
       → downstream service(s) / database
```

Each hop can log the request. The goal: find the **last hop that saw it healthy** and
the **first hop that saw it fail**. The break is between them.

## Workflow

```
Tracer Progress:
- [ ] Reproduce: capture exact method, path, status, body, and a correlation id
- [ ] Collect logs per hop for that correlation id (mesh, app, downstream)
- [ ] Walk hop-by-hop: did the request arrive? did it leave? with what status?
- [ ] Pinpoint the breaking hop; THEN diagnose that hop's root cause
- [ ] Fix the root cause (not just the timeout knob); add a regression check
```

1. **Reproduce & correlate.** Make the call, record the exact `status` + body. Grab a
   **correlation/trace id** (or add one — see [ai-parsable-logging](../ai-parsable-logging/SKILL.md))
   so you can follow one request across hops.
2. **Collect per-hop logs.** For the same correlation id, pull:
   - mesh/sidecar access logs (did the request reach the app? what upstream status?),
   - app pod logs (did the handler run? any exception?),
   - downstream/DB logs or timings.
   Tag each observation with [evidence-ledger](../evidence-ledger/SKILL.md).
3. **Walk the path.** Ask at each hop: *arrived? processed? forwarded? what status
   returned?* The first hop that reports failure (or silence) localizes the break.
4. **Interpret common signatures** (below), then debug that specific hop.

## Signatures → where to look

| Observation | Likely breaking layer | Next step |
|---|---|---|
| 504 at gateway/mesh, **clean app log** (request never arrived or no response in time) | mesh timeout vs. slow/hung app or downstream | compare mesh upstream time to app processing time; fix the slow hop, then the timeout |
| 502/503 at mesh, app pod not ready | app crashed / not healthy / scaling | check pod health/readiness and app startup (see [spring-startup-doctor](../spring-startup-doctor/SKILL.md)) |
| 500 with a stack trace in the app log | application layer | map the trace to the line; handle it; return a structured error |
| 403/401 only for some callers/regions | auth/permission or per-region config at app layer | verify caller permissions/ownership and the region-specific config the pod actually loaded |
| Error only in one region/env | config/topology difference | diff the config the pod loaded per region; look for CORS/origin or endpoint differences |
| Downstream slow → cascading timeout | downstream service / DB (often an N+1) | measure the downstream call; if DB, see [hibernate-nplus1-optimizer](../hibernate-nplus1-optimizer/SKILL.md) |

## Rules of thumb

- **Localize before you fix.** Don't raise a timeout until you've confirmed which hop is
  slow — raising it usually just moves the symptom.
- **One request, one id.** Correlation ids make cross-hop tracing possible; if they're
  missing, that's the first thing to add.
- **Silence is signal.** A hop with *no* log line for the request often means it never
  arrived there — the break is upstream of it.

## Output

"Request broke at **<hop>**: <evidence>. Root cause: <why>. Fix: <change>. Prevention:
<regression test / correlation-id logging>."
