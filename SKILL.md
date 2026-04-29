---
name: html-to-pptx-jsx
description: Create downloadable PowerPoint decks from HTML pages, browser-rendered UI, screenshots, or page descriptions by writing inline browser JSX with @artifact-kit/pptxgenjs-jsx. Use when an agent needs to convert or recreate HTML/web content as editable PPTX slides, especially from a local HTML file, generated web page, dashboard, report, landing page, SVG-heavy slide, or multi-section document.
---

# HTML to PPTX JSX

Use `@artifact-kit/pptxgenjs-jsx` to recreate a page as a declarative PPTX tree inside browser-run HTML. First version rule: do not screenshot the page and do not rasterize HTML/canvas into slides by default. Understand each page or section, then author one JSX `<Slide>` per intended slide and download the PPTX.

## Core Workflow

1. Inspect the source HTML/page enough to understand the content hierarchy, visual grouping, chart/table meaning, SVG primitives, and intended slide boundaries.
2. Create or edit a local HTML file that loads the `@artifact-kit/pptxgenjs-jsx` browser IIFE before Babel Standalone.
3. In an inline `<script type="text/babel" data-type="module" data-presets="typescript,react">`, use Babel classic JSX with `/** @jsx pptxElement */` and read `pptxElement` from `window.ArtifactKitPptxGenJsx`.
4. Build a `<Deck>` with explicit `<Slide>` children. Recreate text, shapes, SVG primitives, images, tables, and charts with package components.
5. Add a download button that calls `validateDeck(deck)` and then `renderPptx(deck, { fileName })`.
6. Serve the HTML over HTTP, open it in a browser, check console errors, then trigger the download.

Start from [assets/browser-inline-jsx-template.html](assets/browser-inline-jsx-template.html) when making a standalone local HTML tool.

## Authoring Rules

- Prefer semantic PPT objects over screenshots: `Text`, `TextRun`, shape components, `Table`, `Image`, and chart components.
- Use one component per PptxGenJS concept; do not call imperative `slide.addText`, `slide.addShape`, or `slide.addChart` unless using the package escape hatch for unsupported behavior.
- Use fixed slide units in inches. For 1600x900 slide-like HTML, use `const PX_PER_IN = 120` and derive `width = 1600 / 120`, `height = 900 / 120`.
- Keep all slide positions explicit: every visible element should have `x`, `y`, `w`, and `h` unless the component docs say otherwise.
- Do not place elements by hand feel. Derive coordinates from source HTML attributes, SVG viewBox values, Tailwind arbitrary classes, or DOM/CSS dimensions, and keep the arithmetic visible in the generated JS.
- For SVG, map simple primitives to editable PPT objects: `rect` -> `Rect`/`RoundRect`, `line/path M-L` -> `Line`, `text` -> `Text`, `circle/ellipse` -> `Ellipse`, and non-trivial `path` -> `CustomGeometry`.
- For charts, prefer native editable PPT charts. Recreate data, chart box, label sizes, legend position, and color series from the HTML/SVG source; exact SVG polyline pixel identity is less important than editability.
- Structure code like React: split top-down into page/section components, implement reusable small components bottom-up, then compose slides.
- Use browser inline JSX only for local authoring or agent workflows. For shipped web apps, precompile with Vite or another build tool.
- Skill examples should use the unversioned CDN URL, or at most a major-version URL if the CDN supports it, so wrapper bugfixes are picked up. Pin an exact package version only for archived deliverables or production workflows after testing.

## Documentation Lookup

When exact components or props matter, read the vendored package docs in this skill in this order:

1. [references/pptxgenjs-jsx-llms.txt](references/pptxgenjs-jsx-llms.txt)
2. [references/pptxgenjs-jsx-quickstart.md](references/pptxgenjs-jsx-quickstart.md)
3. [references/pptxgenjs-jsx-component-selection.md](references/pptxgenjs-jsx-component-selection.md)
4. [references/pptxgenjs-jsx-common-props.md](references/pptxgenjs-jsx-common-props.md)
5. Shape-heavy decks: [references/pptxgenjs-jsx-shape-props.md](references/pptxgenjs-jsx-shape-props.md)
6. Chart-heavy decks: [references/pptxgenjs-jsx-chart-props.md](references/pptxgenjs-jsx-chart-props.md)
7. Full upstream surface: [references/pptxgenjs-jsx-all-upstream-props.md](references/pptxgenjs-jsx-all-upstream-props.md)
8. Machine-readable component list: [references/pptxgenjs-jsx-component-manifest.json](references/pptxgenjs-jsx-component-manifest.json)

If `node_modules/@artifact-kit/pptxgenjs-jsx` exists and may be newer than this skill, prefer its `llms.txt`, `docs/`, and `component-manifest.json` files after reading the skill workflow.

## Browser Inline JSX Pattern

Use this pattern, not `@jsxImportSource`, inside Babel Standalone:

```tsx
/** @jsx pptxElement */
const { Deck, Slide, Text, pptxElement, validateDeck, renderPptx } = window.ArtifactKitPptxGenJsx;

const deck = (
  <Deck title="Generated deck" layout={{ name: "WIDE", width: 13.333, height: 7.5 }}>
    <Slide background={{ color: "FFFFFF" }}>
      <Text x={0.7} y={0.6} w={6} h={0.5} fontSize={24} bold color="111827" margin={0}>
        Slide title
      </Text>
    </Slide>
  </Deck>
);

const issues = validateDeck(deck);
if (!issues.some((issue) => issue.level === "error")) {
  await renderPptx(deck, { fileName: "deck.pptx" });
}
```

For a fuller checklist and conversion heuristics, read [references/html-recreation-guide.md](references/html-recreation-guide.md).
