# HTML Recreation Guide

Use this as broader guidance after reading [measure-first-workflow.md](measure-first-workflow.md) and [coordinate-policy.md](coordinate-policy.md).

## Page Understanding

Before writing JSX, identify:

- Deck purpose and audience.
- Slide boundaries: page, section, viewport, card group, report chapter, or visual state.
- Reading order: title, subtitle, metrics, diagrams, charts, tables, annotations, footer.
- Reusable visual language: typography scale, brand colors, borders, chart colors, and spacing rhythm.
- Elements that should remain editable PPT objects: text, key metrics, icons, SVG primitives, shapes, images, tables, and charts.

Do not chase browser pixel perfection when it destroys editability. Preserve measured structure first, then simplify details deliberately.

## Mapping HTML To PPTX JSX

| HTML/UI pattern | PPTX JSX mapping |
| :-- | :-- |
| Page or major section | `Slide` |
| Heading or label | `Text` |
| Inline rich text | `Text` with `TextRun` children |
| Card, pill, panel, badge | `Rect`, `RoundRect`, or other shape component |
| Divider or rule | `Line`; use `LineBetween` when endpoint direction matters |
| SVG rect/ellipse/line/text | Native shape/text using viewBox mapping |
| SVG path | `CustomGeometry` when editable path geometry matters |
| Image asset | `Image` with measured box |
| Data table | `Table` with rows/cells |
| Bar, line, pie, area chart | Native chart component |
| Unsupported feature | `Raw` escape hatch, with a short reason |

## Slide Construction

- Measure the slide root and use `readSlideLayout`.
- Draw backgrounds and panels before text.
- Use measured boxes for all DOM text.
- Use measured SVG boxes plus source `viewBox` for SVG internals.
- Use native charts when data is recoverable; use measured chart region for `x/y/w/h`.
- Split source content into multiple slides when the native PPT version would be unreadably dense.

## Browser File Pattern

Load runtime before Babel:

```html
<script src="https://unpkg.com/@artifact-kit/pptxgenjs-jsx/dist/pptxgenjs-jsx.browser.iife.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

Use classic JSX:

```html
<script type="text/babel" data-type="module" data-presets="typescript,react">
  /** @jsx pptxElement */
  const { Deck, Slide, Text, pptxElement } = window.ArtifactKitPptxGenJsx;
</script>
```

## Common Failures

- `importSource cannot be set when runtime is classic`: replace `@jsxImportSource` with `/** @jsx pptxElement */`.
- `pptxElement is not a function`: load the IIFE before Babel.
- Blank downloaded deck: ensure the deck is a `Deck` node with `Slide` children.
- Missing browser download: await `renderPptx` inside an async click handler.
- Panel correct but text wrong: mark the text DOM node and read its measured box.
- SVG arrows wrong: use `LineBetween`, not raw `Line` with negative width/height.
