# Website Spec

Build guide for [visualize-idea-website](SKILL.md). Snippets are minimal and current;
adapt, don't paste blindly.

---

## Scaffold

```bash
npm create vite@latest <idea-slug> -- --template react-ts
cd <idea-slug>
npm i @xyflow/react mermaid recharts motion react-router-dom
npm i -D tailwindcss @tailwindcss/vite
```

Tailwind v4 wires in through the Vite plugin (no `tailwind.config.js` needed for basics):

```ts
// vite.config.ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";
export default defineConfig({ plugins: [react(), tailwindcss()] });
```

```css
/* src/index.css */
@import "tailwindcss";

@theme inline {
  --color-bg: oklch(0.98 0 0);
  --color-fg: oklch(0.2 0 0);
  --color-accent: oklch(0.62 0.19 255);
}
```

**shadcn/ui (optional):** `npx shadcn@latest init` then add primitives
(`npx shadcn@latest add card tabs accordion dialog`). Skip if you want zero extra deps.

---

## Theming (dark/light)

Toggle a `dark` class on `<html>`; default from `prefers-color-scheme`. Define tokens
for both and reference via Tailwind utilities (e.g. `bg-[--color-bg] text-[--color-fg]`).
Persist choice in `localStorage`. Keep all colors as tokens so both themes stay
consistent.

---

## Libraries — minimal correct usage

### React Flow (`@xyflow/react`)
Interactive node/flow/dependency diagrams. **Two gotchas:** import its CSS, and give the
wrapper a **fixed size** or nothing renders.

```tsx
import { ReactFlow, Background, Controls } from "@xyflow/react";
import "@xyflow/react/dist/style.css";

const nodes = [
  { id: "1", position: { x: 0, y: 0 }, data: { label: "Idea" } },
  { id: "2", position: { x: 220, y: 80 }, data: { label: "Step" } },
];
const edges = [{ id: "e1-2", source: "1", target: "2", animated: true }];

export default function Flow() {
  return (
    <div style={{ width: "100%", height: 480 }}>
      <ReactFlow nodes={nodes} edges={edges} fitView>
        <Background /><Controls />
      </ReactFlow>
    </div>
  );
}
```

### Mermaid
Flowcharts / sequence / Gantt from text. **Gotchas:** unique id per render;
`mermaid.render()` returns `{ svg, bindFunctions }`; put theme in effect deps.

```tsx
import { useEffect, useRef, useState } from "react";
import mermaid from "mermaid";

export function Mermaid({ chart, theme = "default" }: { chart: string; theme?: string }) {
  const [svg, setSvg] = useState("");
  const idRef = useRef(`m${Math.random().toString(36).slice(2)}`);
  useEffect(() => {
    mermaid.initialize({ startOnLoad: false, theme });
    mermaid.render(idRef.current, chart).then(({ svg }) => setSvg(svg));
  }, [chart, theme]);
  return <div dangerouslySetInnerHTML={{ __html: svg }} />;
}
```

Gantt example for the Timeline module:

```
gantt
  title Roadmap
  dateFormat YYYY-MM-DD
  section Phase 1
  Validate assumption :a1, 2026-01-01, 7d
  Build prototype     :after a1, 14d
```

### Recharts (default charts)
```tsx
import { LineChart, Line, XAxis, YAxis, Tooltip, ResponsiveContainer } from "recharts";
<ResponsiveContainer width="100%" height={280}>
  <LineChart data={data}>
    <XAxis dataKey="name" /><YAxis /><Tooltip />
    <Line type="monotone" dataKey="value" strokeWidth={2} />
  </LineChart>
</ResponsiveContainer>
```

**Chart choice:** Recharts = fast declarative dashboards (default). Chart.js = simple
canvas charts, many data points. visx = fully custom/bespoke viz (most effort).

### Motion (`motion/react`, formerly Framer Motion)
```tsx
import { motion } from "motion/react";
<motion.div
  initial={{ opacity: 0, y: 12 }}
  animate={{ opacity: 1, y: 0 }}
  whileHover={{ scale: 1.02 }}
  transition={{ duration: 0.3 }}
/>
```
Use for route/element entrance, hover micro-interactions, and `whileInView` scroll
reveals (scrollytelling).

---

## Router + module layout

```tsx
import { BrowserRouter, Routes, Route, NavLink } from "react-router-dom";
// routes: / (Overview) /flow /risks /timeline /metrics
```

Shared shell: `<ThemeProvider>` → top nav (NavLink per module) → animated `<main>`
outlet. Build reusable primitives once: `Meter`, `StatCard`, `RiskHeatmapCell`,
`ShowMore`.

---

## Diagram-type → content mapping

| Content | Use |
|---------|-----|
| Process / how it works | React Flow (interactive) or Mermaid flowchart |
| Dependencies between parts | React Flow graph |
| Sequencing over time | Mermaid Gantt / milestone timeline |
| Quantities, trends, comparisons | Recharts bar/line/area |
| Confidence / risk level | radial meter / progress bar |
| Likelihood × impact | risk heatmap grid |
| A-vs-B decision | comparison matrix + decision tree |
| Spatial/logistical | map/journey view |

---

## "Live" polish widgets

- **Confidence meter** — radial gauge or animated bar bound to assumption strength %.
- **Risk heatmap** — 3×3 or 5×5 likelihood × impact grid, cells colored, hover for detail.
- **Animated progress bars** — Motion width transition on mount / scroll-in.
- **KPI tiles** — count-up animation on the number.
- **Interactive filters** — toggle scenarios/segments; charts + meters react live.
- **Verdict badge** — GO / REFINE / NO-GO pill on the overview.

### Show-more convention
```tsx
<details className="group">
  <summary className="cursor-pointer select-none">Show more</summary>
  <div className="mt-2 text-sm opacity-80">{detail}</div>
</details>
```
Default view shows only the headline + visual; everything secondary goes inside.

---

## Surfacing the assumption ledger

The Assumptions & Risks module renders the [evidence-ledger](../evidence-ledger/SKILL.md)
table as cards:
- One card per assumption: statement, **strength meter (0-100%)**, ↑/↓ factors, status chip
  (open / verified / falsified).
- Evidenced facts get a distinct badge/color from assumptions.
- Sort low-strength + high-impact first so the shakiest foundations are most visible.
This is the honesty mechanism — never bury it.

---

## Responsive + verify

- Mobile-first Tailwind utilities; stack modules vertically on small screens; make React
  Flow/heatmaps scroll or shrink gracefully. No horizontal page scroll.
- Before finishing: `npm run dev`, click every route, toggle theme, resize to mobile,
  confirm no console errors, run the SKILL.md polish checklist.
