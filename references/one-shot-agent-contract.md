# One-Shot Agent Contract

Use this contract when an agent must produce a working exporter in one pass. It prevents the common failure mode where the agent writes a final HTML file without decomposition, measurement coverage, or SVG analysis.

## Required Output Shape

A one-shot implementation must contain these sections, either in the agent response or as a top comment in the generated exporter:

```text
HTML_TO_PPTX_EXPORT_PLAN
input: path/to/source.html
exporter: path/to/source-export.html
input_mutation: forbidden

COMPONENT_TREE
Deck
  Slide
    Header
    MainContent
      Panel(...)
      Diagram(...)
    Footer

MEASUREMENT_MANIFEST
id | selector | kind | reason
slide | main.slide | slide-root | layout and px-per-inch
title | h1 | text | native PPT title position and font
main-panel | section.main | container | panel border and children anchor
diagram-svg | svg[data-name="diagram"] | svg | viewBox mapping root

SVG_INVENTORY
svg id | viewBox | primitives | mapping
diagram-svg | 0 0 1040 390 | rect,line,path,text | map primitives to Rect/RoundRect/LineBetween/Text

RASTER_FALLBACKS
none
```

If `SVG_INVENTORY` says an SVG has primitives, the exporter must include mapping helpers and native PPT components for those primitives. It must not use `Image`, `snapdom`, canvas capture, or data URLs for that SVG.

## Implementation Order

1. Inspect source HTML and CSS class structure.
2. Identify slide roots and repeated regions.
3. Create the component tree.
4. Create the measurement manifest.
5. Inspect every SVG source. Record viewBox and primitive groups.
6. Copy the input into the exporter.
7. Add measurement attributes from the manifest.
8. Write componentized inline JSX using the manifest and SVG inventory.
9. Validate, render, and visually compare the downloaded PPTX.

Do not combine steps 1-8 into a single unstructured code dump.

## Componentization Rules

- Use one top-level `buildDeck()` or `<Deck>` declaration.
- Use named functions for major regions: `Header`, `MainPanel`, `Diagram`, `SideCards`, `Footer`.
- Use smaller functions for repeated primitives: `TokenMatrix`, `Arrow`, `FlowNode`, `Legend`, `Callout`.
- Pass measured boxes and source data into components. Do not hide coordinate arithmetic inside unexplained literals.
- Use arrays and `.map()` for repeated cells, bars, labels, and markers.

Good:

```tsx
function Header() {
  return (
    <>
      <Text {...readPptBox("eyebrow")} fontSize={readFontPt("eyebrow")} bold margin={0}>
        {text("eyebrow")}
      </Text>
      <Text {...readPptBox("title")} fontSize={readFontPt("title")} bold margin={0}>
        {text("title")}
      </Text>
    </>
  );
}
```

Bad:

```tsx
<Slide>
  {/* hundreds of unrelated Text/Rect/Line nodes with guessed numbers */}
</Slide>
```

## SVG Native-Mapping Gate

For each SVG, classify primitives before deciding output type:

| SVG primitive | Native PPT target |
| :-- | :-- |
| `rect`, rounded `rect` | `Rect`, `RoundRect` |
| `line`, simple `path M/L` | `LineBetween` |
| `circle`, `ellipse` | `Ellipse` |
| `text` | `Text` |
| polygonal `path` | `CustomGeometry` |
| chart lines/bars/markers with recoverable data | native chart component |

Fallback to raster only when:

- the SVG is a complex filter/texture/illustration whose editability is not useful,
- source geometry is unavailable,
- or native reconstruction would be misleading.

When falling back, write a `RASTER_FALLBACKS` entry with the SVG selector and reason.

## Coordinate Sources

Every coordinate in exporter JSX must come from exactly one of:

- `readPptBox(id)`, `readSlideLayout(id)`, or `readFontPt(id)`;
- SVG `viewBox` formulas from source primitives;
- native chart box measured from DOM plus chart data from source;
- small local padding/inset relative to a measured or SVG-derived box;
- explicit constants copied from source HTML/CSS/Tailwind.

If the coordinate came from "looks close", it is invalid.

