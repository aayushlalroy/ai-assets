---
name: spring-startup-doctor
description: >-
  Diagnoses why a Spring Boot service won't start or won't wire — configuration
  and environment issues (missing properties, wrong profile, unresolved
  placeholders, secrets, truststore/keystore) and bean-creation/autowiring
  failures (BeanCreationException, NoSuchBeanDefinitionException,
  UnsatisfiedDependencyException, @ConfigurationProperties binding). Use when an
  app fails to start locally, "works in the container but not locally", or the
  user mentions "no such bean", "bean creation", "autowire", "config
  placeholder not resolved", "which profile is active", or a startup stack
  trace. Composes clarify-first and evidence-ledger.
disable-model-invocation: true
---

# Spring Startup Doctor

The two most common reasons a Spring Boot service won't come up: **it can't resolve its
configuration**, or **it can't wire its beans**. Work evidence-first — read the *root*
of the stack trace, not the top line.

Detailed symptom → cause → fix tables: [CHECKS.md](CHECKS.md).

## First moves

1. **Clarify the context** (via [clarify-first](../clarify-first/SKILL.md)) if unknown:
   local vs container? which profile? did it ever start? what changed last?
2. **Get the real error.** Read the **bottom-most `Caused by:`** in the stack trace —
   that's the true cause. Tag findings with
   [evidence-ledger](../evidence-ledger/SKILL.md) (`[Evidenced: log line …]`).
3. **Classify** the failure into one of the two families below.

## Family A — Configuration / environment

Symptoms: won't start locally; `Could not resolve placeholder`; wrong/no active
profile; `@ConfigurationProperties` binding failure; truststore/keystore errors;
"works in the container, not locally".

Checklist:
- Confirm the **active profile** (`spring.profiles.active`) is what you expect, and any
  `spring.config.additional-location` / import points at the right config source.
- Verify **every required property** (and any injected secret) is actually present.
  Binding a missing/typed-wrong `@ConfigurationProperties` value fails fast at startup.
- For "works in the container, not locally": **diff the config the running container has
  vs. local.** Dump the effective config from inside the container and compare keys.
- Check TLS material: truststore/keystore **paths** and JVM `-D` options.
- Never hard-code secrets — they should come from an injected env/secret source. If a
  secret is missing locally, supply it via your local mechanism, don't commit it.

## Family B — Bean creation / autowiring

Symptoms: `BeanCreationException`, `NoSuchBeanDefinitionException`,
`UnsatisfiedDependencyException`, circular-dependency errors at startup.

Checklist:
- Read the root cause: *which bean*, *needing which dependency*, *why*.
- Ensure the bean is **component-scanned** (`@Component`/`@Service`/`@Repository`) or
  explicitly declared with `@Bean`, and is on the **active profile**.
- For "no qualifying bean" ambiguity, add `@Qualifier` or mark one `@Primary`.
- For "required a bean that could not be found", check the dependency isn't excluded by
  an auto-configuration condition or a missing starter on the classpath.
- Prefer **constructor injection** (final fields) so missing deps fail clearly at
  construction and are easy to test.
- A `@ConfigurationProperties` bean that fails to bind surfaces here too — cross-check
  Family A.

## Workflow

```
Startup Doctor Progress:
- [ ] Capture the full startup log; find the bottom-most Caused by
- [ ] Classify: Config/Env (A) or Bean/DI (B)
- [ ] Run the matching checklist; confirm root cause with evidence
- [ ] Apply the minimal fix; restart; confirm clean startup
- [ ] Add a guard (fail-fast validation / test) so it can't silently recur
```

## Output

Root cause (quoted from the log) → the specific fix → a one-line prevention (e.g.
"add `@Validated` + required constraints on the properties class so a missing key fails
with a clear message"). See [CHECKS.md](CHECKS.md) for the full lookup tables.
