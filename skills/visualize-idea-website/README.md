# Visualize Idea Website (`visualize-idea-website`)

> [!WARNING]
> **Pre-requisites**:
> - [`clarify-first`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/clarify-first/README.md) (Leaf Skill — clarifies theme, depth, and modules)
> - [`evidence-ledger`](file:///Users/roy.a2yush/Develop/Personal/aayushlalroy/cursor-knowledge-book/assets/skills/evidence-ledger/README.md) (Leaf Skill — surface assumption cards & confidence meters)
> - **Tech Spec**: Includes [`VISUALIZE.md`](VISUALIZE.md) (Vite + Tailwind v4 + React Flow + Mermaid + Recharts + Motion)

---

## What This Skill Does
Generates a diagram-heavy, minimal-text, modular interactive React + Vite + Tailwind website that visualizes an idea across 5 standard routes (Overview dashboard, Flow/Architecture, Assumptions & Risks, Timeline/Roadmap, Metrics).

---

## When to Use

### Triggers & Scenarios
- **Visual Prototyping**: When asked `"visualize my idea"`, `"make a website out of this"`, `"build an interactive diagram"`, or `"show me this idea visually"`.
- **Interactive Pitching**: Surfacing complex technical or product ideas visually instead of long prose docs.

### When NOT to Use
- Do NOT use for production backend service deployments or database migrations.

---

## Examples

### Scaffold Command (from VISUALIZE.md)
```bash
npm create vite@latest idea-visualizer -- --template react-ts
npm i @xyflow/react mermaid recharts motion react-router-dom
```

---

## Axon Import Command

Assuming you are in the `assets/` directory:

```bash
axon add skill skills/visualize-idea-website
```
