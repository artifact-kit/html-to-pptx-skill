# HTML to PPTX JSX Skill

Teach an agent to turn HTML pages into downloadable PowerPoint decks with [`@artifact-kit/pptxgenjs-jsx`](https://github.com/artifact-kit/pptxgenjs-jsx).

The first version is intentionally direct: understand each HTML page or section, derive layout from the source HTML/CSS/SVG where possible, write inline JSX that declares a native PPTX tree, then download the deck in the browser. It does not screenshot the page by default.

## What It Does

- Converts web pages, dashboards, reports, or slide-like HTML into `.pptx` files.
- Uses semantic PowerPoint objects: text boxes, shapes, SVG-derived geometry, lines, tables, images, and charts.
- Runs as a local browser workflow with Babel Standalone and CDN imports.
- Includes vendored component and props docs so agents can use the wrapper without guessing.
- Keeps the core skill short while linking to deeper references only when needed.

## Install As A Skill

Clone this repository into your agent's skill directory:

```bash
git clone https://github.com/artifact-kit/html-to-pptx-jsx.git ~/.codex/skills/html-to-pptx-jsx
```

For other agent runtimes, install the folder wherever that runtime loads `SKILL.md`-based skills. The important files are:

- `SKILL.md`
- `agents/openai.yaml`
- `references/`
- `assets/`

## Runtime Dependency

Generated HTML examples use the published browser IIFE build before Babel. This keeps load order deterministic for local inline JSX:

```html
<script src="https://unpkg.com/@artifact-kit/pptxgenjs-jsx/dist/pptxgenjs-jsx.browser.iife.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

The examples intentionally do not pin a patch version, so wrapper bugfixes reach skill users through the CDN. For archived or production workflows, pin a tested package version after validation.

Inside the inline Babel module, use classic JSX and read components from the global:

```tsx
/** @jsx pptxElement */
const { Deck, Slide, Text, pptxElement, renderPptx, validateDeck } = window.ArtifactKitPptxGenJsx;
```

## Example

This repo includes a concrete HTML-to-PPTX demo:

- Input HTML: [`examples/input/attention-mechanism.html`](examples/input/attention-mechanism.html)
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

Click **Download attention-mechanism.pptx**. The generated PPTX recreates the input slide as native PowerPoint content: selectable text, shape panels, SVG-derived primitive shapes, `CustomGeometry` path geometry, arrowed flow lines, a heatmap built from PPT rectangles, and a native line chart from structured data.

## How Agents Should Use It

When a user asks to convert HTML to PPTX:

1. Read `SKILL.md`.
2. Read `references/html-recreation-guide.md` for conversion heuristics.
3. Read `references/pptxgenjs-jsx-llms.txt`.
4. Load component-specific docs only as needed:
   - Common text/table/image props: `references/pptxgenjs-jsx-common-props.md`
   - Shape props: `references/pptxgenjs-jsx-shape-props.md`
   - Chart props: `references/pptxgenjs-jsx-chart-props.md`
   - Full upstream prop surface: `references/pptxgenjs-jsx-all-upstream-props.md`
5. Start from `assets/browser-inline-jsx-template.html`.
6. Serve the generated HTML over local HTTP and verify browser console/download behavior.

## Design Positioning

This skill is not a screenshot pipeline. It is a production-flow bridge for agents:

- HTML gives the agent the visual and content reference.
- Source HTML/CSS/SVG gives the agent measurable layout constants.
- JSX gives the agent a structured PowerPoint declaration language.
- `@artifact-kit/pptxgenjs-jsx` gives the agent access to PptxGenJS without imperative command ordering.
- The final `.pptx` remains editable, searchable, and reusable.

Future versions can add stronger DOM measurement, `snapdom` screenshot fallbacks, and richer asset extraction. Version one stays deterministic and easy to reason about.
