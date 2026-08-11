# Startup Diagnostics — Symptom → Cause → Fix

Lookup tables for [spring-startup-doctor](SKILL.md). All examples are generic; adapt to
your service.

## Configuration / environment

| Symptom | Likely root cause | Fix |
|---|---|---|
| `Could not resolve placeholder 'x.y.z'` | property not defined for the active profile / missing import | define the key, or point `spring.config.import` / `additional-location` at the source that has it |
| App uses wrong values | wrong `spring.profiles.active` | set the intended profile (env var, `-Dspring.profiles.active`, or IDE run config) |
| `Binding to target ... failed` / `Failed to bind properties` | `@ConfigurationProperties` key missing or wrong type | fix key name/type; add `@Validated` + constraints to fail with a clear message |
| Starts in container, not locally | secrets/config injected in the container but absent locally | dump effective config inside the container, diff against local, supply the missing keys locally |
| `PKIX path building failed` / keystore errors | wrong truststore/keystore path or password, missing cert | fix `-Djavax.net.ssl.trustStore*` paths; import the required cert into your local store |
| Secret is `null` at runtime | secret not injected in this environment | provide it via your local secret mechanism; never hard-code or commit it |

**Fail-fast tip:** annotate properties classes with `@Validated` and put
`@NotNull`/`@NotBlank` on required fields so a missing value stops startup with an
actionable message instead of a later NPE.

## Bean creation / autowiring

| Symptom | Likely root cause | Fix |
|---|---|---|
| `NoSuchBeanDefinitionException` | bean not scanned / not defined / wrong profile | add stereotype or `@Bean`; ensure the package is scanned; check profile |
| `expected single matching bean but found N` | multiple candidates of one type | add `@Qualifier("...")` at the injection point or `@Primary` on one bean |
| `UnsatisfiedDependencyException` | a required dependency higher in the graph failed | read the nested `Caused by`; fix the *root* bean, not the reported one |
| `... required a bean of type '...' that could not be found` | missing starter/dependency, or auto-config condition not met | add the dependency/starter; check `@ConditionalOn...` requirements |
| Circular dependency error | two beans depend on each other via constructors | break the cycle (extract a third bean, or use a setter/`@Lazy` on one edge) |
| `@ConfigurationProperties` bean won't create | binding failure (see Config table) | fix the binding; this often masquerades as a DI error |

**Injection tip:** prefer constructor injection with `final` fields — missing
collaborators fail at construction with a precise message and stay trivially mockable in
tests.

## Universal order

1. Reproduce the startup; capture the **full** log.
2. Jump to the **bottom-most `Caused by:`**.
3. Decide Config vs DI (they overlap for `@ConfigurationProperties`).
4. Apply the smallest fix; restart to confirm.
5. Add a guard (validation/test) so the failure can't silently return.
