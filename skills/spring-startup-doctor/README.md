# Spring Startup Doctor (`spring-startup-doctor`)

> [!WARNING]
> **Pre-requisites**:
> - [`clarify-first`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/clarify-first/README.md) (Leaf Skill — confirms active profiles and local vs container context)
> - [`evidence-ledger`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/evidence-ledger/README.md) (Leaf Skill — tags bottom-most `Caused by:` stack trace evidence)
> - **Lookup Tables**: Includes [`CHECKS.md`](CHECKS.md) (Symptom → Cause → Fix lookup tables)

---

## What This Skill Does
Orchestrates diagnosis and resolution for Spring Boot startup failures, categorizing errors into Family A (Configuration/Environment placeholders and profiles) or Family B (BeanCreationException and autowiring dependency injection).

---

## When to Use

### Triggers & Scenarios
- **Startup Stack Traces**: When a Spring Boot app fails to launch locally or in container environments.
- **Autowiring / Config Issues**: `"no such bean"`, `"unresolved placeholder"`, `"BeanCreationException"`.

### When NOT to Use
- Do NOT use for HTTP 500 runtime business logic exceptions after successful application boot.

---

## Examples

### Stack Trace Analysis & Classification
```
Caused by: org.springframework.beans.factory.NoSuchBeanDefinitionException: No qualifying bean of type 'com.example.UserService' available
-> Category: Family B (Bean Wiring)
-> Fix: Verify @Service annotation and component scan package path.
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/spring-startup-doctor
```
