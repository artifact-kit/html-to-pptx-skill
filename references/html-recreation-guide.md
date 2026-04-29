# HTML Recreation Guide

## Scope

Use this reference when turning a source HTML page, local app, screenshot, or page description into a PPTX-producing HTML file. The first version does semantic recreation only: no DOM measurement, no computed style extraction, no canvas rendering, and no screenshot fallback.

## Page Understanding

Before writing JSX, identify:

- Deck purpose and audience.
- Slide boundaries: one source page, section, viewport, card group, report chapter, or visual state can become one slide.
- Reading order: title, subtitle, primary metric, chart, table, annotations, footer.
- Reusable visual language: typography scale, brand colors, border style, chart colors, and spacing rhythm.
- Elements that should be native PPT objects: text, key metrics, icons, shapes, images, tables, charts.

Do not chase pixel-perfect HTML layout. Aim for a clean PowerPoint-native reconstruction that preserves hierarchy, data, and visual intent.

## Mapping HTML to PPTX JSX

| HTML/UI pattern | PPTX JSX mapping |
| :-- | :-- |
| Page or major section | `<Slide>` |
| Heading or label | `<Text>` |
| Inline rich text | `<Text>` with `<TextRun>` children |
| Card, pill, panel, badge | Shape component such as `<Rect>` or `<RoundRect>` |
| Divider or rule | `<Line>` |
| Image or screenshot asset | `<Image>` with explicit sizing |
| Data table | `<Table>` with rows/cells |
| Bar, line, pie, area chart | `BarChart`, `LineChart`, `PieChart`, `AreaChart`, etc. |
| Unsupported PptxGenJS feature | `RawSlide` or package escape hatch, with comments explaining why |

## Slide Construction Heuristics

- Start with a global coordinate plan. For wide slides, use `13.333 x 7.5`.
- Reserve margins first: often `0.5-0.8` inches on each side.
- Place titles at top-left. Keep title `h` stable, usually `0.35-0.7`.
- Build large background bands and cards before text.
- Give charts and tables more space than the HTML source if the slide would otherwise feel cramped.
- Convert tiny web UI labels into fewer PowerPoint annotations when the exact UI chrome is not important.
- Keep footer/source text small but readable, usually `7-10` pt.

## Browser File Pattern

For local inline JSX, load the browser IIFE before Babel so the runtime is ready before Babel executes transformed JSX:

```html
<script src="https://unpkg.com/@artifact-kit/pptxgenjs-jsx@0.1.0/dist/pptxgenjs-jsx.browser.iife.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

Inside the Babel script, use classic runtime:

```html
<script type="text/babel" data-type="module" data-presets="typescript,react">
  /** @jsx h */
  const { Deck, Slide, Text, h, validateDeck, renderPptx } = window.ArtifactKitPptxGenJsx;
</script>
```

Do not use `/** @jsxImportSource @artifact-kit/pptxgenjs-jsx */` with Babel Standalone unless the React preset is explicitly configured for automatic runtime. The classic `h` pattern is the default for this skill.

## Validation Checklist

- The HTML page loads over `http://localhost` or `http://127.0.0.1`, not `file://`, when using module imports.
- Browser console has no JavaScript errors.
- `validateDeck(deck)` reports no `error` issues before rendering.
- The download button calls `renderPptx(deck, { fileName })`.
- Generated deck opens in PowerPoint/Keynote/LibreOffice without repair prompts.
- Text is selectable in the PPTX when it came from semantic text, not an image.

## Common Failures

- `importSource cannot be set when runtime is classic`: replace `@jsxImportSource` with `/** @jsx h */` and import `h`.
- `h is not a function`: load `pptxgenjs-jsx.browser.iife.js` before Babel and read `h` from `window.ArtifactKitPptxGenJsx`.
- `Failed to resolve module specifier`: use the IIFE pattern above, or add/fix the import map entry for `@artifact-kit/pptxgenjs-jsx` if intentionally using ESM.
- Blank downloaded deck: ensure the `deck` variable is a `<Deck>` node with `<Slide>` children.
- Missing browser download: ensure the click handler is async and awaits `renderPptx`.
- Overcrowded slide: split the source section into multiple slides instead of shrinking all text.
