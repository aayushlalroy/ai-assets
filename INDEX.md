# Assets Index & Import Directory

> **Master Navigation & Axon Import Registry**  
> All commands assume working directory is the `assets/` root folder.

---

## 1. Principles (`assets/principles/`)

| Principle | Description | File Link | Axon Import Command | Prerequisites |
| :--- | :--- | :--- | :--- | :--- |
| **skill-attribution** | Requires every response to end with a footer listing skills used. | [`skill-attribution.md`](principles/skill-attribution.md) | `axon add principle principles/skill-attribution.md` | None |
| **claim-tagging** | Tags claims inline as `[Evidenced: source]` or `[Assumption NN%: reasoning]`. | [`claim-tagging.md`](principles/claim-tagging.md) | `axon add principle principles/claim-tagging.md` | None |
| **token-attribution** | Appends user/agent/output token usage breakdown to turn footers. | [`token-attribution.md`](principles/token-attribution.md) | `axon add principle principles/token-attribution.md` | None |
| **doc-version-sync-policy** | Requires updating docs (README, CHANGELOG, CRQ) and bumping SemVer version for all code changes. | [`doc-version-sync-policy.md`](principles/doc-version-sync-policy.md) | `axon add principle principles/doc-version-sync-policy.md` | None |

---

## 2. Leaf Primitive Skills (`assets/skills/`)

| Skill | Description | README Link | Axon Import Command | Prerequisites Warning |
| :--- | :--- | :--- | :--- | :--- |
| **clarify-first** | Asks structured multiple-choice questions with recommended options before execution. | [`README.md`](skills/clarify-first/README.md) | `axon add skill skills/clarify-first` | None |
| **evidence-ledger** | Tags claims as Evidenced vs Assumption and maintains an ordered confidence ledger. | [`README.md`](skills/evidence-ledger/README.md) | `axon add skill skills/evidence-ledger` | None |
| **ai-parsable-logging** | Configures structured JSON logging with correlation IDs for jq tracing. | [`README.md`](skills/ai-parsable-logging/README.md) | `axon add skill skills/ai-parsable-logging` | None |
| **hibernate-nplus1-optimizer** | Diagnoses and collapses JPA/Hibernate N+1 SELECT queries into set-based joins. | [`README.md`](skills/hibernate-nplus1-optimizer/README.md) | `axon add skill skills/hibernate-nplus1-optimizer` | ⚠️ Requires `evidence-ledger` |
| **git-recovery-runbook** | Emergency runbook for git reflog recoveries, rebase fixes, and safety resets. | [`README.md`](skills/git-recovery-runbook/README.md) | `axon add skill skills/git-recovery-runbook` | ⚠️ Requires `clarify-first` |
| **request-layer-tracer** | Localizes failing API requests across gateway, mesh sidecars, app pods, and databases. | [`README.md`](skills/request-layer-tracer/README.md) | `axon add skill skills/request-layer-tracer` | ⚠️ Requires `ai-parsable-logging`, `evidence-ledger` |
| **test-coverage-booster** | Generates targeted JUnit 5 + Mockito tests to boost branch coverage. | [`README.md`](skills/test-coverage-booster/README.md) | `axon add skill skills/test-coverage-booster` | None |
| **openapi-contract-first** | Designs REST APIs contract-first in `api-spec/` using modular `$ref` JSON schemas. | [`README.md`](skills/openapi-contract-first/README.md) | `axon add skill skills/openapi-contract-first` | None (Includes `schema-code-sync.md`) |
| **bruno-request-generator** | Generates ready-to-run curl commands and Bruno (`.bru`) API collections. | [`README.md`](skills/bruno-request-generator/README.md) | `axon add skill skills/bruno-request-generator` | ⚠️ Requires `clarify-first` |
| **jira-tech-story-drafter** | Drafts plan-first technical user stories, acceptance criteria, and design specs. | [`README.md`](skills/jira-tech-story-drafter/README.md) | `axon add skill skills/jira-tech-story-drafter` | None |
| **scrutinize-idea** | Single-pass red-teaming using steel-man, pre-mortem, and ICE/RICE scoring. | [`README.md`](skills/scrutinize-idea/README.md) | `axon add skill skills/scrutinize-idea` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `CRITIQUE.md` |
| **visualize-idea-website** | Generates modular React + Vite visual idea prototype websites. | [`README.md`](skills/visualize-idea-website/README.md) | `axon add skill skills/visualize-idea-website` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `VISUALIZE.md` |
| **skill-improvement-log** | Appends proposed skill improvements to a persistent human-reviewed backlog. | [`README.md`](skills/skill-improvement-log/README.md) | `axon add skill skills/skill-improvement-log` | ⚠️ Requires `evidence-ledger` |
| **create-skill-from-formatted** | Audits and token-optimizes existing or pre-formatted `SKILL.md` files. | [`README.md`](skills/create-skill-from-formatted/README.md) | `axon add skill skills/create-skill-from-formatted` | ⚠️ Requires `skill-metadata-optimizer` |
| **create-skill-from-prompt** | Formats raw prompt ideas into structured `SKILL.md` spec files. | [`README.md`](skills/create-skill-from-prompt/README.md) | `axon add skill skills/create-skill-from-prompt` | ⚠️ Requires `skill-metadata-optimizer` |
| **create-skill-from-workflow** | Distills executed conversation transcripts into reusable `SKILL.md` specs. | [`README.md`](skills/create-skill-from-workflow/README.md) | `axon add skill skills/create-skill-from-workflow` | ⚠️ Requires `skill-metadata-optimizer` |
| **skill-metadata-optimizer** | Evaluates and token-optimizes `SKILL.md` frontmatter (< 50 words). | [`README.md`](skills/skill-metadata-optimizer/README.md) | `axon add skill skills/skill-metadata-optimizer` | None |
| **doc-version-sync** | Synchronizes README/CHANGELOG/CRQs, calculates SemVer bumps, and flags breaking changes or stale data risks. | [`README.md`](skills/doc-version-sync/README.md) | `axon add skill skills/doc-version-sync` | None |

---

## 3. Orchestrator Skills (`assets/skills/`)

| Skill | Description | README Link | Axon Import Command | Prerequisites Warning |
| :--- | :--- | :--- | :--- | :--- |
| **spring-startup-doctor** | Diagnoses Spring Boot startup & bean autowiring failures. | [`README.md`](skills/spring-startup-doctor/README.md) | `axon add skill skills/spring-startup-doctor` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `CHECKS.md` |
| **pr-review-principal** | Principal-engineer PR review (contract, errors, security, N+1). | [`README.md`](skills/pr-review-principal/README.md) | `axon add skill skills/pr-review-principal` | ⚠️ Requires `openapi-contract-first`, `hibernate-nplus1-optimizer`, `test-coverage-booster` |
| **adversarial-review-loop** | Multi-round Worker/Reviewer/Manager adversarial review loop. | [`README.md`](skills/adversarial-review-loop/README.md) | `axon add skill skills/adversarial-review-loop` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `skill-improvement-log`, `pr-review-principal`, `PROMPTS.md` |
| **skill-creator** | Master orchestrator for creating skills from formatted files, prompts, or workflows. | [`README.md`](skills/skill-creator/README.md) | `axon add skill skills/skill-creator` | ⚠️ Requires `create-skill-from-formatted`, `create-skill-from-prompt`, `create-skill-from-workflow`, `skill-metadata-optimizer` |

---

## 4. Workflows (`assets/skills/`)

| Workflow | Description | README Link | Axon Import Command | Prerequisites Warning |
| :--- | :--- | :--- | :--- | :--- |
| **idea-lab** | 4-Phase idea incubator (Clarify -> Scrutinize -> Harden -> Prototype). | [`README.md`](skills/idea-lab/README.md) | `axon add skill skills/idea-lab` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `scrutinize-idea`, `adversarial-review-loop`, `visualize-idea-website` |

---

## Community Resources & Blog Posts

* 📦 **[ai-assets Repository](https://github.com/aayushlalroy/ai-assets)** — Official community repository containing production-ready skills, principles, and workflows.
* 📦 **[Axon Repository](https://github.com/aayushlalroy/axon)** — Official source code and documentation for Axon CLI.
* ✍️ **[Axon CLI Blog Post](https://www.roya2yush.com/writing/axon-ai-agent-skill-management)** — Deep dive into Axon's skill and constitution management system.
* ✍️ **[AI Assets Blog Post](https://www.roya2yush.com/writing/ai-assets-production-ready-agent-skills)** — Guide to production-ready agent skills and principles.
* 🧠 **[Skills, Principles & Workflows Architecture](https://www.roya2yush.com/writing/ai-agent-skills-principles-workflows-architecture)** — Architectural guide explaining how skills, principles, and workflows operate together.

