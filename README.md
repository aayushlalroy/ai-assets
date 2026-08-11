# assets/ — drop-in, reusable artifacts

The **portable payload** of the knowledge book: the concrete files you copy into a
new machine or agent to work *your* way from day one. Unlike the numbered root docs
(which *describe* how the engineer works), everything here is meant to be **used
directly**.

## What's inside

| Path | What it is |
| --- | --- |
| `AGENTS.md` | A drop-in conventions/rules file — copy to a project root or `~/.cursor/AGENTS.md` so an agent adopts the engineer's standards immediately. |
| `skills/` | The canonical, portable `SKILL.md` agent skills (engineering runbooks + the idea-lab suite). See [`skills/README.md`](skills/README.md). |
| `personal-ai-dataset.jsonl` | 1,549 anonymized instruction→response pairs distilled from real sessions. Datasheet: [`../11-personal-ai-dataset.md`](../11-personal-ai-dataset.md). *(Gitignored pending review.)* |

## How this differs from other folders

- **vs. the numbered root docs (`00`–`12`)** — those are *prose about* the engineer;
  this folder holds the *machine-usable artifacts* (rules file, skills, dataset).
- **vs. `skills/` (top level)** — `assets/skills/` are hand-authored **engineering +
  idea-lab** skills you invoke directly. The top-level [`skills/`](../skills/) folder is a
  separate **chat-mining refresh pipeline**. Different purpose, no overlap.
- **vs. `bootstrap/`** — `bootstrap/` is only the *installer* that copies `AGENTS.md`
  and `skills/` onto a new box; the sources of truth live here.

## Duplicate notes

- `personal-ai-dataset.jsonl` is the **data**; `local-ai-assistant/` adds a *runnable
  retrieval layer* over it (intentional, additive — not a copy).
- `assets/skills/` is copied into `publishing/skills-pack/skills/` for public release.
  That copy is intentional (adds an MIT license + catalog for distribution); the
  originals here remain the source of truth.
