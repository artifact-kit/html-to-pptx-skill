# Audit Checklist

Run this checklist before handing off an HTML-to-PPTX exporter.

## Workflow Alignment

- The original input HTML was copied first and remains read-only.
- The exporter is a separate HTML file.
- Every slide/page is visible in one top-to-bottom container in the exporter copy.
- Hidden, inactive, virtualized, carousel-only, or `display:none` slides are made measurable before export.
- The exporter has one visible export button or toolbar.
- The exporter uses the CDN browser build plus inline Babel JSX.
- No package install, Node export script, CLI exporter, server renderer, or screenshot-only pipeline was introduced unless the user explicitly requested it.

## Source Hygiene

- The original input HTML has no generated export button.
- The original input HTML has no `data-ak-*`, `data-artifact-kit-*`, or `data-slide-container` measurement markers.
- Measurement markers exist only in the generated exporter copy.

Useful check:

```bash
rg "data-ak-|data-artifact-kit|data-slide-container" examples/input
```

This should return nothing for clean input fixtures.

## Measurement Coverage

The exporter should mark:

- Each slide root.
- Header title/subtitle/eyebrow.
- Major panels/cards.
- Panel titles.
- Body text blocks and captions.
- SVG containers.
- Chart containers.
- Footer text blocks.

Any DOM-derived PPT object without a marker is suspicious. Add `data-ak-measure` and use `readPptBox` rather than visual coordinates.

## Coordinate Audit

Search exporter code:

```bash
rg "readPptBox|readSlideLayout|readFontPt|x1=|y1=|x=\\{|y=\\{|w=\\{|h=\\{" examples/generated
```

Every remaining coordinate must be explained as one of:

- `readPptBox` / `readSlideLayout` / `readFontPt`.
- Explicit source HTML/CSS/Tailwind value.
- SVG viewBox primitive mapping.
- Small local label inset inside a measured or SVG-derived object.

If the reason is "it looked right", replace it with a marker and measurement.

## Browser Runtime

- Runtime script loads before Babel.
- Inline Babel uses `/** @jsx pptxElement */`.
- `measureArtifacts({ document })` runs inside the export click handler before reading boxes.
- `validateDeck(deck)` runs before `renderPptx`.
- Console has no JavaScript errors.

## PPTX Output

Open the downloaded deck in PowerPoint/WPS/Keynote/LibreOffice:

- Deck opens without repair prompts.
- Text from HTML is selectable.
- Major panels align with source.
- Text blocks do not overlap.
- SVG arrows preserve direction.
- Charts are native when data is available.
- Any image fallback is intentional and documented in code.

## API Legality

- No invented chart types such as `heatmap`.
- Generic `Chart` is used only when the desired chart type is valid and no dedicated chart component is a better fit.
- `LineChart`, `BarChart`, `PieChart`, etc. use props from `pptxgenjs-jsx-chart-props.md`.
- `LineBetween` calls provide numeric `x1`, `y1`, `x2`, and `y2`. They do not spread `readPptBox(...)`.
- Source cards, badges, connectors, icons, matrices, and decorative shapes are represented by shapes where practical, not only by `Text`.

## Failure Signs

- The source HTML was modified instead of copied.
- The exporter only exposes one active slide and leaves the rest hidden.
- The exporter uses measurement tags but the export code does not call `measureArtifacts`.
- The exporter uses component names, chart types, or props that do not appear in the wrapper docs.
- SVGs were embedded as PNG/data URLs even though their primitives are readable.
- SVG text was recreated manually while boxes, arrows, or matrices were rasterized.
- Many coordinates are bare numbers unrelated to measurement, viewBox math, or source CSS.

## Common Fixes

- Text shifted inside panels: mark the specific text node and use `readPptBox`, not panel-relative guesses.
- Panel size correct but internals wrong: mark inner SVG/text/caption nodes separately.
- Arrow direction wrong: use `LineBetween`.
- `line.endpoint.invalid`: do not spread `x/y/w/h` boxes into `LineBetween`; compute endpoint points.
- `Chart type` failure: check valid chart types; heatmaps are shape grids, not charts.
- SVG path too large: convert path points to local geometry coordinates, not raw SVG coordinates.
- Blank image in PPT: prefer native shapes; use image fallback only after testing the actual downloaded PPTX.
