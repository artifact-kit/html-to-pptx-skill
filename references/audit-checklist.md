# Audit Checklist

Run this checklist before handing off an HTML-to-PPTX exporter.

## Stage Gates

- The work includes a file plan naming the clean input and generated exporter.
- The work includes a component tree. A single monolithic slide function is not acceptable for complex pages.
- The work includes a measurement manifest with ids, selectors, kinds, and reasons.
- The work includes an SVG inventory for every source SVG.
- The work includes a raster fallback list. Empty is fine; undocumented image fallback is not.

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

- Slide root.
- Header title/subtitle/eyebrow.
- Major panels/cards.
- Panel titles.
- Body text blocks and captions.
- SVG containers.
- Chart containers.
- Footer text blocks.

Any DOM-derived PPT object without a marker is suspicious.

If the exporter contains PPT text or shapes for a DOM block but the DOM block is absent from the manifest, add a marker and use `readPptBox`.

## Coordinate Audit

Search exporter code:

```bash
rg "x: inch\\(|y: inch\\(|w: inch\\(|h: inch\\(|at\\(|pptBox\\(|x=\\{|y=\\{" examples/generated
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

## One-Shot Failure Signs

- The agent only created `output.html` and did not show or embed a component tree.
- The exporter has measurement tags but no manifest explaining coverage.
- SVGs were embedded as PNG/data URLs without an SVG inventory.
- SVG text was recreated manually while boxes, arrows, or matrices were rasterized.
- Many coordinates are bare numbers unrelated to measurement, viewBox math, or source CSS.

## Common Fixes

- Text shifted inside panels: mark the specific text node and use `readPptBox`, not panel-relative guesses.
- Panel size correct but internals wrong: mark inner SVG/text/caption nodes separately.
- Arrow direction wrong: use `LineBetween`.
- SVG path too large: convert path points to local geometry coordinates, not raw SVG coordinates.
- Blank image in PPT: prefer native shapes; use image fallback only after testing the actual downloaded PPTX.
