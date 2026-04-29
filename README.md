# HTML to PPTX JSX Skill

Teach an agent to turn HTML pages into downloadable, editable PowerPoint decks with [`@artifact-kit/pptxgenjs-jsx`](https://github.com/artifact-kit/pptxgenjs-jsx).

This skill is measure-first: keep the source HTML clean, copy it into an exporter page, add DOM measurement markers to the exporter, and generate native PPTX objects from measured boxes plus SVG source geometry.

## What It Does

- Converts web pages, dashboards, reports, or slide-like HTML into `.pptx`.
- Preserves editability with native PowerPoint text, shapes, lines, tables, images, and charts.
- Uses `data-ak-measure` and `readPptBox()` so agents do not guess DOM coordinates.
- Maps SVG primitives from `viewBox` coordinates into editable PPT shapes.
- Uses raster fallback only when native reconstruction is not practical.
- Includes vendored component/props docs so agents can use the JSX wrapper without guessing.

## Install As A Skill

Clone this repository into your agent's skill directory:

```bash
git clone https://github.com/artifact-kit/html-to-pptx-jsx.git ~/.codex/skills/html-to-pptx-jsx
```

For other agent runtimes, install the folder wherever that runtime loads `SKILL.md`-based skills.

## Runtime Pattern

Generated exporters use the published browser IIFE before Babel:

```html
<script src="https://unpkg.com/@artifact-kit/pptxgenjs-jsx/dist/pptxgenjs-jsx.browser.iife.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

Inside the inline Babel module:

```tsx
/** @jsx pptxElement */
const {
  Deck,
  Slide,
  Text,
  measureArtifacts,
  pptxElement,
  readPptBox,
  readSlideLayout,
  renderPptx,
  validateDeck,
} = window.ArtifactKitPptxGenJsx;
```

## Example

This repo includes a concrete measure-first demo:

- Clean input: [`examples/input/attention-mechanism.html`](examples/input/attention-mechanism.html)
- Generated exporter: [`examples/generated/attention-pptx-export.html`](examples/generated/attention-pptx-export.html)

Run it locally:

```bash
cd html-to-pptx-jsx
python3 -m http.server 4178
```

Open:

```text
http://127.0.0.1:4178/examples/generated/attention-pptx-export.html
```

Click **Export PPTX**. The exporter measures its own DOM, recreates the slide with native PowerPoint objects, validates the deck, and downloads a `.pptx`.

## Agent Workflow

1. Read `SKILL.md`.
2. Read `references/measure-first-workflow.md`.
3. Read `references/coordinate-policy.md`.
4. Load component docs only as needed.
5. Before handoff, run through `references/audit-checklist.md`.

## Design Positioning

This is not a screenshot pipeline. It is a production-flow bridge for agents:

- HTML provides the visual and content reference.
- DOM measurement provides reliable layout.
- SVG source provides precise primitive geometry.
- JSX provides a structured PowerPoint declaration language.
- `@artifact-kit/pptxgenjs-jsx` exposes PptxGenJS through LLM-friendly components.
