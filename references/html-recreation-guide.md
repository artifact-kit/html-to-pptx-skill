# HTML Recreation Guide

## Scope

Use this reference when turning a source HTML page, local app, screenshot, or page description into a PPTX-producing HTML file. The default output should be editable, semantic PowerPoint content. Do not screenshot/rasterize the page by default. Use DOM/CSS/source-derived dimensions when available, and keep the arithmetic in the generated JS so another agent can audit the conversion.

## Page Understanding

Before writing JSX, identify:

- Deck purpose and audience.
- Slide boundaries: one source page, section, viewport, card group, report chapter, or visual state can become one slide.
- Reading order: title, subtitle, primary metric, chart, table, annotations, footer.
- Reusable visual language: typography scale, brand colors, border style, chart colors, and spacing rhythm.
- Elements that should be native PPT objects: text, key metrics, icons, SVG primitives, shapes, images, tables, charts.

Do not chase pixel-perfect browser rendering when it would destroy editability. Do preserve source geometry: use exact source numbers and formulas where the HTML/SVG/Tailwind source exposes them.

## Coordinate And Sizing Rules

- If the source is slide-like `1600px x 900px`, use `const PX_PER_IN = 120`, `const inch = (px) => px / PX_PER_IN`, and `layout={{ name: "SRC_1600_900", width: inch(1600), height: inch(900) }}`.
- Convert every source pixel box through a helper such as `pptBox({ x, y, w, h })`; do not write final inch coordinates directly unless the source is already in inches.
- Prefer dimensions from source code in this order: explicit HTML/SVG attributes, Tailwind arbitrary classes such as `w-[1600px]`, CSS rules, DOM/CSS computed values, then screenshot/manual approximation only when no structural source exists.
- Keep relationships as formulas: `mainW = slideW - margin * 2 - asideW - gap`, `panelY = headerY + headerH + 16`, `cellX = gridX + col * cell`.
- Only copy absolute numbers that explicitly appear in the source HTML/CSS/SVG or are documented constants in the conversion.

## SVG Primitive Mapping

For SVG inside the source HTML, treat the SVG as a coordinate system and map primitives into editable PPT objects.

```ts
const mapSvgX = (svg, value) => svg.abs.x + (value - svg.viewBox.x) * (svg.abs.w / svg.viewBox.w);
const mapSvgY = (svg, value) => svg.abs.y + (value - svg.viewBox.y) * (svg.abs.h / svg.viewBox.h);
const svgBox = (svg, box) => pptBox({
  x: mapSvgX(svg, box.x),
  y: mapSvgY(svg, box.y),
  w: box.w * (svg.abs.w / svg.viewBox.w),
  h: box.h * (svg.abs.h / svg.viewBox.h),
});
```

| SVG pattern | PPTX JSX mapping |
| :-- | :-- |
| `<rect>` with `rx` | `<RoundRect>` using mapped `x/y/w/h` |
| `<rect>` without `rx` | `<Rect>` |
| `<line>` or `path d="M x y L x y"` | `<Line>` with mapped endpoints |
| `<text>` | `<Text>` at mapped anchor box; use source font size scaled by the SVG render scale |
| `<circle>` / `<ellipse>` | `<Ellipse>` |
| `<path>` with `M/L/H/V/C/Q/Z` | `<CustomGeometry>` with local `points` |
| Complex filters, gradients, unsupported paths | Prefer semantic simplification; use image fallback only when editability is impossible |

For `CustomGeometry`, compute the path bounding box in SVG coordinates, map that bbox to slide `x/y/w/h`, then subtract the bbox origin from every path point so `points` are local:

```tsx
<CustomGeometry
  {...svgBox(svg, pathBBox)}
  points={[
    { x: 0, y: 0, moveTo: true },
    { x: 40, y: 0 },
    { x: 56, y: 18 },
    { x: 40, y: 36 },
    { x: 0, y: 36 },
    { close: true },
  ]}
  fill={{ color: "08265F" }}
  line={{ color: "08265F", transparency: 100 }}
/>
```

This corresponds to an SVG path like `M 120 40 L 160 40 L 176 58 L 160 76 L 120 76 Z` with `pathBBox = { x: 120, y: 40, w: 56, h: 36 }`.

## Mapping HTML to PPTX JSX

| HTML/UI pattern | PPTX JSX mapping |
| :-- | :-- |
| Page or major section | `<Slide>` |
| Heading or label | `<Text>` |
| Inline rich text | `<Text>` with `<TextRun>` children |
| Card, pill, panel, badge | Shape component such as `<Rect>` or `<RoundRect>` |
| Divider or rule | `<Line>` |
| SVG rect/ellipse/line/text | Matching native PPT shape/text component with viewBox mapping |
| SVG path | `<CustomGeometry>` when editable path geometry matters |
| Image or screenshot asset | `<Image>` with explicit sizing |
| Data table | `<Table>` with rows/cells |
| Bar, line, pie, area chart | `BarChart`, `LineChart`, `PieChart`, `AreaChart`, etc. |
| Unsupported PptxGenJS feature | `RawSlide` or package escape hatch, with comments explaining why |

## Slide Construction Heuristics

- Start with a global coordinate plan. For 1600x900 HTML, derive `13.333 x 7.5` from `1600 / 120` and `900 / 120`.
- Reserve margins first: often `0.5-0.8` inches on each side.
- Place titles at top-left. Keep title `h` stable, usually `0.35-0.7`.
- Build large background bands and cards before text.
- Give charts and tables more space than the HTML source if the slide would otherwise feel cramped.
- Convert tiny web UI labels into fewer PowerPoint annotations when the exact UI chrome is not important.
- Keep footer/source text small but readable, usually `7-10` pt.

## Browser File Pattern

For local inline JSX, load the browser IIFE before Babel so the runtime is ready before Babel executes transformed JSX:

```html
<script src="https://unpkg.com/@artifact-kit/pptxgenjs-jsx/dist/pptxgenjs-jsx.browser.iife.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

Use the unversioned CDN URL in skill examples so bugfixes in the wrapper become available automatically. Pin an exact package version only for archived deliverables or production workflows after testing.

Inside the Babel script, use classic runtime:

```html
<script type="text/babel" data-type="module" data-presets="typescript,react">
  /** @jsx pptxElement */
  const { Deck, Slide, Text, pptxElement, validateDeck, renderPptx } = window.ArtifactKitPptxGenJsx;
</script>
```

Do not use `/** @jsxImportSource @artifact-kit/pptxgenjs-jsx */` with Babel Standalone unless the React preset is explicitly configured for automatic runtime. The classic `pptxElement` pattern is the default for this skill because it avoids shadowing PptxGenJS `h` height props.

## Validation Checklist

- The HTML page loads over `http://localhost` or `http://127.0.0.1`, not `file://`, when using module imports.
- Browser console has no JavaScript errors.
- `validateDeck(deck)` reports no `error` issues before rendering.
- The download button calls `renderPptx(deck, { fileName })`.
- Generated deck opens in PowerPoint/Keynote/LibreOffice without repair prompts.
- Text is selectable in the PPTX when it came from semantic text, not an image.

## Common Failures

- `importSource cannot be set when runtime is classic`: replace `@jsxImportSource` with `/** @jsx pptxElement */` and use `pptxElement`.
- `pptxElement is not a function`: load `pptxgenjs-jsx.browser.iife.js` before Babel and read `pptxElement` from `window.ArtifactKitPptxGenJsx`.
- `Failed to resolve module specifier`: use the IIFE pattern above, or add/fix the import map entry for `@artifact-kit/pptxgenjs-jsx` if intentionally using ESM.
- Blank downloaded deck: ensure the `deck` variable is a `<Deck>` node with `<Slide>` children.
- Missing browser download: ensure the click handler is async and awaits `renderPptx`.
- Overcrowded slide: split the source section into multiple slides instead of shrinking all text.
