---
name: visualize-idea-website
description: >-
  Generates a diagram-heavy, minimal-text interactive website to visualize an idea across multiple routes. Trigger on user prompt ("visualize my idea", "make a website out of this", "build interactive diagram", "show idea visually") or workflow events (post-scrutiny visual prototyping). Do NOT trigger for backend production service deployments.
disable-model-invocation: true
---

# Visualize Idea Website

Turn a (preferably already-scrutinized) idea into a site the user can *see and click
through*. Diagrams over prose, split across routes, alive with motion.

Full stack setup, code snippets, module templates, and polish checklist:
[VISUALIZE.md](VISUALIZE.md).

## Principles (non-negotiable)

- **Diagram-heavy, minimal text.** Every point is shown — flows, charts, dashboards,
  maps, timelines. Prose is the exception.
- **Progressive disclosure.** Secondary detail hides behind "show more" (`<details>` /
  accordion / drawer). Default view stays scannable.
- **Modular / multi-route.** Split across pages — never one long scroll-dump. Each
  module is its own route.
- **Live feel.** Animated transitions, interactive filters, hover states, live-updating
  meters and progress bars.
- **Honest visuals.** Surface the assumption ledger and risks — pretty charts must not
  hide weak logic.

## Workflow

```
Visualize Progress:
- [ ] Clarify (clarify-first): audience, purpose, which modules, theme, depth
- [ ] Pick module subset (default: the five below)
- [ ] Scaffold (Vite + Tailwind v4 + libs)
- [ ] Build shared shell: theme provider, nav, layout, meter/card primitives
- [ ] Build modules one route at a time, wired to real idea + ledger content
- [ ] Polish + verify (runs, responsive, theme, no console errors)
```

1. **Clarify** via [clarify-first](../clarify-first/SKILL.md): audience, purpose, which
   modules matter, dark/light default, and how deep to go.
2. **Scaffold** per VISUALIZE.md (exact commands there).
3. **Build shell first**, then modules one route at a time.
4. Wire content from the refined idea and the
   [evidence-ledger](../evidence-ledger/SKILL.md) — assumptions become visual cards +
   confidence meters.
5. **Verify** against the polish checklist; run it and fix console/lint errors.

## Default stack (with escape hatches)

- **React + Vite + TypeScript** — fast scaffold, HMR.
- **Tailwind CSS v4** — utility styling + dark/light theming via CSS tokens.
- **React Flow (`@xyflow/react`)** — interactive node/flow/dependency diagrams.
- **Mermaid** — quick flowcharts / sequence / Gantt from text.
- **Recharts** — charts/dashboards (default). *Escape:* Chart.js (simple canvas charts),
  visx (bespoke viz).
- **Motion (`motion/react`)** — animations & micro-interactions.
- **shadcn/ui** — optional, for polished primitives (cards, tabs, accordion, dialog).

*Lighter escape hatch:* for a simple idea or when speed matters, a single-file static
site (one HTML + CDN Mermaid + Chart.js) is fine — keep the diagram-heavy, minimal-text,
progressive-disclosure principles.

## Standard modules (routes)

Default to these five; add situational ones as fitting.

1. **Overview dashboard** (`/`) — idea at a glance: hero one-liner, verdict badge,
   confidence + risk meters, KPI tiles, links into modules.
2. **Flow / Architecture** (`/flow`) — how it works: React Flow or Mermaid diagram;
   interactive nodes reveal detail.
3. **Assumptions & Risks** (`/risks`) — the ledger made visual: assumption cards with
   strength meters, risk heatmap (likelihood × impact), pre-mortem board. Honesty lives here.
4. **Timeline / Roadmap** (`/timeline`) — sequencing/dependencies (Gantt or milestones).
5. **Metrics / Decision** (`/metrics`) — cost/effort dashboard, option-comparison matrix,
   ICE/RICE score visualized, live progress bars, scenario filters.

Situational: **Map/Journey** (spatial/logistical ideas), **Options Explorer**
(decision matrix + tree), **Budget** dashboard.

## Polish checklist

```
- [ ] Dark/light theme toggle, respects system preference
- [ ] Responsive (mobile → desktop), no horizontal scroll
- [ ] Animated route/element transitions (Motion)
- [ ] Interactive: hover, filters, clickable diagram nodes
- [ ] "Show more" disclosures for all secondary detail
- [ ] Confidence + risk meters on the overview
- [ ] Graceful loading/empty states
- [ ] Runs (npm run dev) with no console errors
```

## Composition

- Uses [clarify-first](../clarify-first/SKILL.md) for audience/scope/theme decisions.
- Uses [evidence-ledger](../evidence-ledger/SKILL.md) — the Assumptions & Risks module
  renders the ledger with confidence meters.
- Best run after [scrutinize-idea](../scrutinize-idea/SKILL.md) so it visualizes the
  *refined* idea; orchestrated by [idea-lab](../idea-lab/SKILL.md).
