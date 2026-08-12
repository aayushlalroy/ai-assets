# AI Assets (`ai-assets`)

**AI Assets** is a community repository of production-ready **Skills**, **Principles**, and **Workflows** for AI coding agents (Cursor, Claude Code, Gemini/Antigravity, Devin, Codex, Windsurf, GitHub Copilot).

Instead of authoring instructions from scratch, copy or import these drop-in artifacts to give your agents immediate domain expertise, engineering standards, and robust runbooks.

---

## ⚡ Fast Track: Import & Manage with Axon CLI

The fastest and cleanest way to import and deploy these assets across your projects is using [**Axon**](https://github.com/aayushlalroy/axon), the universal skill management CLI.

### 1. Bulk Import All Assets into Axon

Clone this repository and run `axon import` using the bundled manifest (`axon-import.yaml`):

```bash
# Clone the repository
git clone https://github.com/aayushlalroy/ai-assets.git
cd ai-assets

# Bulk-import all skills, principles, and workflows into central hub (~/.axon/)
axon import . --config axon-import.yaml
```

Once imported into `~/.axon/`, all assets are staged centrally.

### 2. Enable in Any Project

Navigate to any of your project repositories and enable the assets you need:

```bash
cd /path/to/your-project

# Initialize agent directory layouts
axon init

# Enable principles & skills for your active agents
axon enable principle skill-attribution
axon enable skill clarify-first
```

### 3. Stage Individual Assets

You can also stage individual items directly from this repository without bulk importing:

```bash
# Stage a single principle
axon add principles/skill-attribution.md --type principle

# Stage a single skill
axon add skills/clarify-first --type skill
```

---

## 📂 Repository Layout & Index

For the full catalog of pre-built assets, exact CLI import commands, descriptions, and prerequisite dependencies, consult the master navigation index:

👉 [**INDEX.md**](./INDEX.md) — **Master Catalog & Import Registry**

### Directory Structure

| Path | Description |
|---|---|
| 📋 [**INDEX.md**](./INDEX.md) | Master index listing all Principles, Leaf Primitive Skills, Orchestrator Skills, and Workflows with single-command `axon add` instructions. |
| 📜 [**principles/**](./principles/) | Flat Markdown rules (always-on constitutions) like `skill-attribution.md`, `claim-tagging.md`, and `doc-version-sync-policy.md`. |
| 🛠️ [**skills/**](./skills/) | Standard `SKILL.md` folders containing specialized engineering skills (e.g. `clarify-first`, `evidence-ledger`, `spring-startup-doctor`, `pr-review-principal`). |
| ⚙️ [**axon-import.yaml**](./axon-import.yaml) | Pre-configured manifest file for bulk importing all assets via `axon import . --config axon-import.yaml`. |

---

## 📚 Articles & Learning Resources

Learn how to design, manage, and scale agent skill libraries and constitutions:

* 📦 [**Axon CLI Repository**](https://github.com/aayushlalroy/axon) — Universal Skill & Constitution Management System for AI coding agents.
* 📦 [**AI Assets Repository**](https://github.com/aayushlalroy/ai-assets) — Official open-source catalog of production-ready agent skills.
* ✍️ [**Axon CLI Blog Post**](https://www.roya2yush.com/writing/axon-ai-agent-skill-management) — How Axon manages skill staging, symlinking, and multi-agent compatibility.
* ✍️ [**AI Assets Blog Post**](https://www.roya2yush.com/writing/ai-assets-production-ready-agent-skills) — Deep dive into authoring production-ready skills and principles.
* 🧠 [**Skills, Principles & Workflows Architecture**](https://www.roya2yush.com/writing/ai-agent-skills-principles-workflows-architecture) — Comprehensive architectural breakdown of skills, principles, and workflows.

---

## License

[MIT](./LICENSE) © Aayush Lal Roy
