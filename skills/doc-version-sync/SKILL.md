---
name: doc-version-sync
description: >-
  Synchronizes documentation (README, CHANGELOG, CRQs), calculates SemVer bumps (MAJOR/MINOR/PATCH), and flags breaking API changes or stale data upgrade risks after code edits. Trigger on user prompt ("bump version", "update changelog", "sync docs and version") or workflow events (post-code modification). Do NOT trigger for read-only repository inspection.
disable-model-invocation: false
---

# Document & Version Synchronization (`doc-version-sync`)

Synchronize project documentation, compute Semantic Versioning (`MAJOR.MINOR.PATCH`) bumps, and explicitly flag breaking changes or stale data upgrade risks whenever code changes occur.

## Execution Workflow

```
Doc & Version Sync Progress:
- [ ] Inspect git diff to categorize code changes
- [ ] Determine Semantic Version bump (PATCH vs MINOR vs MAJOR)
- [ ] Audit for breaking changes, stale data conflicts, and upgrade risks
- [ ] Update project version manifest (package.json / pyproject.toml / pom.xml / version file)
- [ ] Update README.md, CHANGELOG.md, and release/CRQ notes
- [ ] Summarize version bump and upgrade flags for the user
```

---

## 1. Semantic Versioning Rules (`MAJOR.MINOR.PATCH`)

Evaluate the changes in `git diff` against these criteria:

### `PATCH` (vX.Y.Z → vX.Y.Z+1)
- **Scope**: Small, backward-compatible bug fixes, minor performance tweaks, documentation edits, or internal refactoring.
- **Criteria**: No new public API methods or properties introduced; no breaking behavior.

### `MINOR` (vX.Y.Z → vX.Y+1.0)
- **Scope**: Backward-compatible new features, new public endpoints/methods, or added optional configuration parameters.
- **Criteria**: Expands functionality without breaking existing consumers or contract interfaces.

### `MAJOR` (vX.Y.Z → vX+1.0.0)
- **Scope**: Incompatible API changes, removed endpoints/methods, renamed fields, schema restructuring, or major architectural shifts.
- **Criteria**: Any change requiring existing clients/consumers to modify their code or data models.

---

## 2. Incompatibility & Upgrade Risk Audit (Mandatory Flags)

Whenever analyzing changes, explicitly audit and flag the following risk categories:

### A. Incompatible API & Contract Changes
- **Flag**: `⚠️ BREAKING CHANGE`
- **Scenarios**: Removed endpoints/methods, altered parameter types, mandatory header additions, or renamed JSON fields.
- **Action**: Force `MAJOR` version bump. Document the exact breaking signature and migration path.

### B. Stale Data & Cache Conflicts
- **Flag**: `⚠️ STALE DATA / CACHE RISK`
- **Scenarios**: Changes to serialized object shapes, database schemas, cached data keys, or local storage structures.
- **Action**: Document cache invalidation steps, database migration scripts, or steps to prevent conflicts caused by existing stale data during upgrade.

---

## 3. Documentation Update Checklist

1. **Project Version File**: Update the version tag in `package.json`, `pyproject.toml`, `pom.xml`, `build.gradle`, or `VERSION` file.
2. **`README.md`**: Update usage instructions, parameters, or API signatures if public interfaces changed.
3. **`CHANGELOG.md`**: Prepend a dated entry under `## [vX.Y.Z] - YYYY-MM-DD`:
   - Group entries into: `Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`, and `Breaking Changes`.
   - Highlight any `⚠️ STALE DATA RISK` or manual migration requirements.
4. **Release Notes / CRQ Summary**: Draft a brief release summary suitable for Change Request / Deployment documentation.

---

## 4. Output Summary Template

After applying updates, output a summary report:

```markdown
### 🚀 Version Sync Complete: `v1.2.3` -> `v1.3.0` (MINOR Bump)

- **SemVer Reason**: Added new `/v1/shares` pagination parameter (backward-compatible).
- **Files Updated**: `pyproject.toml`, `CHANGELOG.md`, `README.md`.
- **Incompatibility Check**: `Clean` (No breaking API changes).
- **Upgrade / Stale Data Risk**: `⚠️ CACHE RISK` — Redis key format updated; flush cache key pattern `shares:*` upon deployment.
```
