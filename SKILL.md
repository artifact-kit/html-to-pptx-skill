---
name: html-to-pptx-jsx
description: Create downloadable, editable PowerPoint decks from HTML pages by copying the source into a browser exporter page, laying slides out vertically, measuring DOM nodes, and using the CDN browser build of @artifact-kit/pptxgenjs-jsx with inline JSX. Use for local HTML files, generated web pages, dashboards, reports, slide-like Tailwind pages, SVG-heavy pages, or any workflow that needs HTML-to-PPTX reconstruction with DOM measurement rather than guessed coordinates.
---

# HTML to PPTX JSX

Turn rendered HTML into an editable PPTX in the browser. The intended workflow is not a build pipeline: copy the original HTML, make the copy an exporter, lay every slide/page out vertically, measure rendered nodes, recreate each page with `@artifact-kit/pptxgenjs-jsx` JSX, and export from a button.

## Required Path

Follow this sequence. Do not substitute a Node script, CLI exporter, server-side renderer, package install, Vite app, webpack build, or screenshot-only pipeline unless the user explicitly asks for that different workflow.

1. **Copy the original file.** Treat the source HTML as read-only. Create a separate exporter HTML next to it, for example `name.pptx-export.html`.
2. **Flatten the slides in the copy.** If the original is a slideshow, carousel, route, tab set, or deck runtime, expand it so every slide/page is visible in one top-to-bottom container. Hidden, virtualized, inactive, or `display:none` slides must be made measurable in the exporter copy.
3. **Add one export button.** Put a fixed toolbar/button in the exporter copy only. Keep the original content visible for visual comparison.
4. **Use the CDN browser library.** Load the CDN IIFE build of `@artifact-kit/pptxgenjs-jsx` and Babel Standalone directly in the exporter page. Do not run `pnpm install`, `npm install`, or create a Node export script just to make a PPTX.
5. **Add measurement attributes.** Mark each slide root with `data-ak-slide`, `data-ak-width`, `data-ak-height`, and `data-ak-px-per-in`. Mark each DOM element needed in PPT with `data-ak-measure="stable-id"`.
6. **Measure in the click handler.** Inside the export button handler, call `await measureArtifacts({ document })`, then use `readSlideLayout(id)`, `readPptBox(id)`, and `readFontPt(id)` for slide layout, placement, and text sizing.
7. **Recreate each page with inline JSX.** Use `window.ArtifactKitPptxGenJsx` components to build editable PPT content from measured boxes and source geometry. Create one `<Slide>` per visible HTML slide/page.
8. **Validate and export.** Run `validateDeck(deck)`. If no errors are present, call `renderPptx(deck, { fileName })`. Open the downloaded PPTX and compare it against the exporter page when the environment allows.

## Required Reading

Read these before coding the exporter JSX:

1. `examples/generated/attention-pptx-export.html` for the intended end-to-end exporter shape.
2. `assets/browser-inline-jsx-template.html` for the minimal CDN + Babel pattern.
3. `references/pptxgenjs-jsx-measure-contract.md` for `data-ak-*`, `measureArtifacts`, `readPptBox`, `readFontPt`, and `readSlideLayout`.
4. `references/pptxgenjs-jsx-component-selection.md` for component names and when to use them.
5. `references/pptxgenjs-jsx-common-props.md` for shared position, text, fill, line, image, and table props.
6. `references/pptxgenjs-jsx-shape-props.md` when rebuilding SVG/diagram primitives.
7. `references/pptxgenjs-jsx-chart-props.md` when using native charts.
8. `references/pptxgenjs-jsx-component-manifest.json` when uncertain whether a component or prop exists.

Read only when relevant:

- `references/svg-viewbox-mapping.md` for SVG-heavy pages.
- `references/native-reconstruction-patterns.md` for cards, diagrams, heatmaps, icons, arrows, and repeated UI patterns.
- `references/audit-checklist.md` before final delivery.
- `references/pptxgenjs-jsx-all-upstream-props.md` only when focused props docs do not answer a question.

If local `node_modules/@artifact-kit/pptxgenjs-jsx` already exists and appears newer than this skill, prefer its `llms.txt`, `docs/`, and `component-manifest.json`. Do not install it just to check docs.

## Browser Inline Pattern

Use this pattern in the copied exporter page:

```html
<script src="https://unpkg.com/@artifact-kit/pptxgenjs-jsx/dist/pptxgenjs-jsx.browser.iife.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel" data-presets="typescript,react">
  /** @jsx pptxElement */
  const {
    Deck,
    Slide,
    Text,
    Rect,
    RoundRect,
    LineBetween,
    measureArtifacts,
    pptxElement,
    readFontPt,
    readPptBox,
    readSlideLayout,
    renderPptx,
    validateDeck,
  } = window.ArtifactKitPptxGenJsx;

  document.querySelector("#export-pptx").addEventListener("click", async () => {
    await measureArtifacts({ document });

    const deck = (
      <Deck title="Measured deck" layout={readSlideLayout("slide-1")}>
        <Slide background={{ color: "FFFFFF" }}>
          <Text {...readPptBox("title-1")} fontSize={readFontPt("title-1")} bold margin={0}>
            {document.querySelector('[data-ak-measure="title-1"]').textContent.trim()}
          </Text>
        </Slide>
      </Deck>
    );

    const issues = validateDeck(deck);
    if (issues.some((issue) => issue.level === "error")) throw new Error(JSON.stringify(issues, null, 2));
    await renderPptx(deck, { fileName: "export.pptx" });
  });
</script>
```

Do not use `@jsxImportSource` in inline Babel unless the React preset is explicitly configured for automatic runtime. The default inline-browser pattern is `/** @jsx pptxElement */`.

## Measurement Rules

- Measure rendered DOM, not guesses. Any DOM-derived PPT element needs a `data-ak-measure` id and `readPptBox(id)`.
- Every slide root must declare source pixels and pixel-to-inch ratio, for example `data-ak-width="1600" data-ak-height="900" data-ak-px-per-in="120"`.
- Keep slides visible for measurement. Avoid `display:none`, zero scale, inactive carousel pages, and virtualization in the exporter copy.
- Read measurement values after `await measureArtifacts({ document })`, not at module parse time.
- Keep derived geometry as visible formulas so the mapping is auditable.

## Reconstruction Rules

- Prefer editable native PPT objects over screenshots.
- Rebuild SVG primitives from the source `viewBox`: `rect` -> `Rect`/`RoundRect`, `circle/ellipse` -> `Ellipse`, `line/polyline/path arrows` -> `LineBetween`, text -> `Text`, complex paths -> `CustomGeometry` when practical.
- Use `LineBetween` with numeric `x1`, `y1`, `x2`, `y2`; do not pass it a measured box.
- Valid native chart types are `area`, `bar`, `bar3D`, `bubble`, `doughnut`, `line`, `pie`, `radar`, and `scatter`. Do not use `heatmap`; rebuild heatmaps or matrices with editable `Rect` grids or `Table` cells.
- Use image fallback only for details that cannot be reasonably represented as editable PPT objects, and state the reason.
- Split complex JSX into small functions/components. Avoid one giant unreadable slide function.

## Delivery Checklist

Before final response:

1. Confirm the source file was not modified.
2. Confirm the exporter copy contains a vertical slide/page container and export button.
3. Confirm the CDN browser build is used and no package install or Node export script was introduced.
4. Confirm `measureArtifacts`, `readPptBox`, `readFontPt`, and `readSlideLayout` are used in the export flow.
5. Confirm `validateDeck` runs before `renderPptx`.
6. Confirm the downloaded PPTX was opened or otherwise visually checked when the environment allows it.
