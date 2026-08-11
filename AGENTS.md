# AGENTS.md — Engineering Conventions (portable)

> Distilled from an engineer's real, observed practices. Drop this into a project
> root (or `.cursor/rules/`, `CLAUDE.md`, etc.) to make an AI assistant work the
> way I work. Generic and anonymized — no employer- or project-specific names.

## Golden rules

1. **Contract-first.** Design/modify the OpenAPI or GraphQL schema before code.
   Keep spec ⇄ entities/DTOs ⇄ examples ⇄ generated classes in sync. The spec is
   the source of truth.
2. **Match the existing codebase.** Mirror the current patterns, naming, and
   structure. Consistency beats personal preference. Don't introduce a new style.
3. **Tests are part of done.** Every change includes tests; keep existing tests
   green; aim for maximal meaningful coverage. Fix broken tests, don't delete
   them (unless the behavior is intentionally removed).
4. **Stay in scope.** Do exactly what's asked. Don't refactor unrelated code.
   Call out anything out-of-scope instead of silently doing it.
5. **Evidence over guesses.** Base changes on `git diff`, real logs, and the
   actual generated SQL/code — not assumptions.

## Java / Spring

- Use **constructor injection** (final fields); never field injection.
- Keep the **Controller → Service → Repository** layering; thin controllers, logic
  in services, data access in repositories.
- Prefer `Optional<T>` for maybe-absent values; prefer concise idioms
  (`Set.of(...)`, streams, try-with-resources).
- When a type changes, **propagate it across the whole codebase and its tests**.

## APIs

- Keep request/response schemas as separate files referenced by `$ref`.
- Every error uses **`application/problem+json`** with `type`/`title`/`detail`.
- Enforce field constraints: `required`, `minLength`/`maxLength`,
  `minimum`/`maximum`, `format`. Keep examples valid.
- Version endpoints (`/v1`, `/v2`) for breaking changes; don't break existing
  consumers. Lint the spec.

## Persistence

- JPA entities for the model; **native queries + projections** for hot paths
  (select only needed columns, map to the response shape).
- **Watch for N+1** in the generated SQL; consolidate with joins.
- Model composite keys explicitly. Include audit fields
  (creation/updation time, creator/updater).
- PATCH updates validate an explicit allow-list of patch paths.

## Testing

- JUnit + Mockito. Reproduce a bug with a failing test before fixing it.
- Add tests for every new branch and every changed behavior.

## Git / PR

- Feature branches, rebased on main before merge; prefer clean history.
- Review like a **principal engineer**: verify contract vs. entity vs. data model,
  not just the diff. Use automated review/security tooling in the loop.

## Security

- Secrets come from a secrets manager / injected config — never hard-coded.
- Take SCA/SAST findings seriously; watch for dependency conflicts with the
  framework BOM.
- Validate ownership/permissions on all mutating operations.

## Process

- For large work, write a **plan/design doc first**, then implement against it;
  don't edit the plan mid-implementation.
- Update docs when behavior changes.

## How to talk to me

- Be specific and cite the file/line/log that proves a point.
- Explain the mechanism, not just the fix (e.g. "here's the SQL this generates").
- Respect stated scope boundaries strictly.
