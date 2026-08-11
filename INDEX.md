# Assets Index & Import Directory

> **Master Navigation & Axon Import Registry**  
> Powered by [Axon CLI](https://github.com/aayushlalroy/axon) (`/Users/roy.a2yush/Develop/Personal/opensource/aayushlalroy/axon`).  
> All commands assume working directory is the `ai-assets/` root folder.

---

## 1. Principles (`principles/`)

| Principle | Description | File Link | Axon Import Command | Prerequisites |
| :--- | :--- | :--- | :--- | :--- |
| **skill-attribution** | Requires every response to end with a footer listing skills used. | [`skill-attribution.md`](principles/skill-attribution.md) | `axon add principles/skill-attribution.md --type principle --name skill-attribution` | None |
| **claim-tagging** | Tags claims inline as `[Evidenced: source]` or `[Assumption NN%: reasoning]`. | [`claim-tagging.md`](principles/claim-tagging.md) | `axon add principles/claim-tagging.md --type principle --name claim-tagging` | None |
| **token-attribution** | Appends user/agent/output token usage breakdown to turn footers. | [`token-attribution.md`](principles/token-attribution.md) | `axon add principles/token-attribution.md --type principle --name token-attribution` | None |

---

## 2. Leaf Primitive Skills (`skills/`)

| Skill | Description | README Link | Axon Import Command | Prerequisites Warning |
| :--- | :--- | :--- | :--- | :--- |
| **clarify-first** | Asks structured multiple-choice questions with recommended options before execution. | [`README.md`](skills/clarify-first/README.md) | `axon add skills/clarify-first --type skill --name clarify-first` | None |
| **evidence-ledger** | Tags claims as Evidenced vs Assumption and maintains an ordered confidence ledger. | [`README.md`](skills/evidence-ledger/README.md) | `axon add skills/evidence-ledger --type skill --name evidence-ledger` | None |
| **ai-parsable-logging** | Configures structured JSON logging with correlation IDs for jq tracing. | [`README.md`](skills/ai-parsable-logging/README.md) | `axon add skills/ai-parsable-logging --type skill --name ai-parsable-logging` | None |
| **hibernate-nplus1-optimizer** | Diagnoses and collapses JPA/Hibernate N+1 SELECT queries into set-based joins. | [`README.md`](skills/hibernate-nplus1-optimizer/README.md) | `axon add skills/hibernate-nplus1-optimizer --type skill --name hibernate-nplus1-optimizer` | ⚠️ Requires `evidence-ledger` |
| **git-recovery-runbook** | Emergency runbook for git reflog recoveries, rebase fixes, and safety resets. | [`README.md`](skills/git-recovery-runbook/README.md) | `axon add skills/git-recovery-runbook --type skill --name git-recovery-runbook` | ⚠️ Requires `clarify-first` |
| **request-layer-tracer** | Localizes failing API requests across gateway, mesh sidecars, app pods, and databases. | [`README.md`](skills/request-layer-tracer/README.md) | `axon add skills/request-layer-tracer --type skill --name request-layer-tracer` | ⚠️ Requires `ai-parsable-logging`, `evidence-ledger` |
| **test-coverage-booster** | Generates targeted JUnit 5 + Mockito tests to boost branch coverage. | [`README.md`](skills/test-coverage-booster/README.md) | `axon add skills/test-coverage-booster --type skill --name test-coverage-booster` | None |
| **openapi-contract-first** | Designs REST APIs contract-first in `api-spec/` using modular `$ref` JSON schemas. | [`README.md`](skills/openapi-contract-first/README.md) | `axon add skills/openapi-contract-first --type skill --name openapi-contract-first` | None (Includes `schema-code-sync.md`) |
| **bruno-request-generator** | Generates ready-to-run curl commands and Bruno (`.bru`) API collections. | [`README.md`](skills/bruno-request-generator/README.md) | `axon add skills/bruno-request-generator --type skill --name bruno-request-generator` | ⚠️ Requires `clarify-first` |
| **jira-tech-story-drafter** | Drafts plan-first technical user stories, acceptance criteria, and design specs. | [`README.md`](skills/jira-tech-story-drafter/README.md) | `axon add skills/jira-tech-story-drafter --type skill --name jira-tech-story-drafter` | None |
| **scrutinize-idea** | Single-pass red-teaming using steel-man, pre-mortem, and ICE/RICE scoring. | [`README.md`](skills/scrutinize-idea/README.md) | `axon add skills/scrutinize-idea --type skill --name scrutinize-idea` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `CRITIQUE.md` |
| **visualize-idea-website** | Generates modular React + Vite visual idea prototype websites. | [`README.md`](skills/visualize-idea-website/README.md) | `axon add skills/visualize-idea-website --type skill --name visualize-idea-website` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `VISUALIZE.md` |
| **skill-improvement-log** | Appends proposed skill improvements to a persistent human-reviewed backlog. | [`README.md`](skills/skill-improvement-log/README.md) | `axon add skills/skill-improvement-log --type skill --name skill-improvement-log` | ⚠️ Requires `evidence-ledger` |
| **create-skill-from-formatted** | Audits and token-optimizes existing or pre-formatted `SKILL.md` files. | [`README.md`](skills/create-skill-from-formatted/README.md) | `axon add skills/create-skill-from-formatted --type skill --name create-skill-from-formatted` | ⚠️ Requires `skill-metadata-optimizer` |
| **create-skill-from-prompt** | Formats raw prompt ideas into structured `SKILL.md` spec files. | [`README.md`](skills/create-skill-from-prompt/README.md) | `axon add skills/create-skill-from-prompt --type skill --name create-skill-from-prompt` | ⚠️ Requires `skill-metadata-optimizer` |
| **create-skill-from-workflow** | Distills executed conversation transcripts into reusable `SKILL.md` specs. | [`README.md`](skills/create-skill-from-workflow/README.md) | `axon add skills/create-skill-from-workflow --type skill --name create-skill-from-workflow` | ⚠️ Requires `skill-metadata-optimizer` |
| **skill-metadata-optimizer** | Evaluates and token-optimizes `SKILL.md` frontmatter (< 50 words). | [`README.md`](skills/skill-metadata-optimizer/README.md) | `axon add skills/skill-metadata-optimizer --type skill --name skill-metadata-optimizer` | None |

---

## 3. Orchestrator Skills (`skills/`)

| Skill | Description | README Link | Axon Import Command | Prerequisites Warning |
| :--- | :--- | :--- | :--- | :--- |
| **spring-startup-doctor** | Diagnoses Spring Boot startup & bean autowiring failures. | [`README.md`](skills/spring-startup-doctor/README.md) | `axon add skills/spring-startup-doctor --type skill --name spring-startup-doctor` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `CHECKS.md` |
| **pr-review-principal** | Principal-engineer PR review (contract, errors, security, N+1). | [`README.md`](skills/pr-review-principal/README.md) | `axon add skills/pr-review-principal --type skill --name pr-review-principal` | ⚠️ Requires `openapi-contract-first`, `hibernate-nplus1-optimizer`, `test-coverage-booster` |
| **adversarial-review-loop** | Multi-round Worker/Reviewer/Manager adversarial review loop. | [`README.md`](skills/adversarial-review-loop/README.md) | `axon add skills/adversarial-review-loop --type skill --name adversarial-review-loop` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `skill-improvement-log`, `pr-review-principal`, `PROMPTS.md` |
| **skill-creator** | Master orchestrator for creating skills from formatted files, prompts, or workflows. | [`README.md`](skills/skill-creator/README.md) | `axon add skills/skill-creator --type skill --name skill-creator` | ⚠️ Requires `create-skill-from-formatted`, `create-skill-from-prompt`, `create-skill-from-workflow`, `skill-metadata-optimizer` |

---

## 4. Workflows (`skills/`)

| Workflow | Description | README Link | Axon Import Command | Prerequisites Warning |
| :--- | :--- | :--- | :--- | :--- |
| **idea-lab** | 4-Phase idea incubator (Clarify ➔ Scrutinize ➔ Harden ➔ Prototype). | [`README.md`](skills/idea-lab/README.md) | `axon add skills/idea-lab --type workflow --name idea-lab` | ⚠️ Requires `clarify-first`, `evidence-ledger`, `scrutinize-idea`, `adversarial-review-loop`, `visualize-idea-website` |
