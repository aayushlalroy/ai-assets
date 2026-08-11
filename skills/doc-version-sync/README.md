# Document & Version Synchronization (`doc-version-sync`)

> [!NOTE]
> **Pre-requisites**: None (Leaf Skill)

---

## What This Skill Does
`doc-version-sync` analyzes code changes via `git diff`, calculates the appropriate Semantic Version bump (`MAJOR.MINOR.PATCH`), audits for breaking API changes and stale data/cache risks, and synchronizes project documentation (`README.md`, `CHANGELOG.md`, version manifests, release/CRQ notes).

---

## When to Use

### Triggers & Scenarios
- **Post-Code Modification**: Automatically triggered after completing feature implementations, bug fixes, or architectural refactors.
- **Manual Versioning Prompts**: When asked `"bump version"`, `"update changelog"`, `"sync docs and version"`, or `"prepare release notes"`.

### When NOT to Use
- Do NOT use for read-only repository exploration, plain code reviews, or when no code changes have occurred.

---

## Examples

### Example 1: Minor Feature Release Output
```markdown
### 🚀 Version Sync Complete: `v1.2.0` ➔ `v1.3.0` (MINOR Bump)

- **SemVer Reason**: Added optional `page_size` parameter to share search API.
- **Files Updated**: `package.json`, `CHANGELOG.md`, `README.md`.
- **Incompatibility Check**: `Clean` (Backward-compatible).
- **Upgrade / Stale Data Risk**: `None`.
```

### Example 2: Major Release with Breaking Change & Stale Cache Warning
```markdown
### 🚀 Version Sync Complete: `v1.3.0` ➔ `v2.0.0` (MAJOR Bump)

- **SemVer Reason**: Removed deprecated `user_id` query parameter in favor of JWT context.
- **Files Updated**: `pyproject.toml`, `CHANGELOG.md`, `README.md`.
- **Incompatibility Check**: `⚠️ BREAKING CHANGE` — API callers using `?user_id=` must migrate to Bearer authorization headers.
- **Upgrade / Stale Data Risk**: `⚠️ STALE DATA RISK` — Invalidate local session storage keys (`auth_session_*`) post-deployment.
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/doc-version-sync
```
