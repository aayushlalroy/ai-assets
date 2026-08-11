# AI Assets — Portable Skills, Principles & Agent Artifacts

This repository contains the canonical, portable AI skills, principles, and workflows designed for modern AI coding agents (Cursor, Claude Code, Gemini/Antigravity, Devin, Codex, Windsurf, GitHub Copilot).

It is powered by **[Axon](https://github.com/aayushlalroy/axon)** — the universal Skill & Constitution Management System for AI coding agents.

---

## Quick Start: Staging & Enabling Assets with Axon

### 1. Install Axon CLI

```bash
curl -sSL https://raw.githubusercontent.com/aayushlalroy/axon/main/install.sh | bash
```

For source installation or repository reference:
- GitHub: [https://github.com/aayushlalroy/axon](https://github.com/aayushlalroy/axon)
- Local repository path: `/Users/roy.a2yush/Develop/Personal/opensource/aayushlalroy/axon`

### 2. Bulk Import All Assets into Axon

Bulk stage all skills, principles, and workflows using the pre-configured import manifest:

```bash
axon import . --config axon-import.yaml
```

### 3. Enable for Your Project

Enable all staged assets in your active workspace (e.g., Cursor, Claude Code, Devin):

```bash
axon init                             # Scaffolds target directories for all agents
axon enable --all --agent cursor      # Enable for Cursor
axon enable --all --agent claude      # Enable for Claude Code
axon enable --all --agent gemini      # Enable for Gemini/Antigravity
```

---

## Directory Structure

| Path | Description |
| --- | --- |
| `principles/` | Always-on coding rules (e.g., `claim-tagging.md`, `skill-attribution.md`, `token-attribution.md`). |
| `skills/` | On-demand AgentSkills (`SKILL.md` layout) covering engineering runbooks and the `idea-lab` suite. |
| `axon-import.yaml` | Pre-configured bulk import manifest for `axon import`. |
| `INDEX.md` | Master Navigation Registry with individual `axon add` commands per skill. |

---

## Staging Individual Skills / Principles

To stage an individual item manually into Axon:

```bash
# Stage a single skill:
axon add skills/clarify-first --type skill --name clarify-first

# Stage a single principle:
axon add principles/claim-tagging.md --type principle --name claim-tagging

# Stage a workflow:
axon add skills/idea-lab --type workflow --name idea-lab
```

See [`INDEX.md`](./INDEX.md) for the complete list of individual staging commands and skill dependencies.

---

## License

MIT © Aayush Lal Roy
