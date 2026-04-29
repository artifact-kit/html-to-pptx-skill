# DOM Measure Contract

This contract is for HTML-to-PPTX workflows where the source HTML is rendered in a browser and the deck is authored with `@artifact-kit/pptxgenjs-jsx`.

The public package provides a basic browser fallback. Internal/private runtimes can replace it by exposing the same `window.ArtifactKitMeasure` interface.

## Attribute Contract

Mark the slide container:

```html
<main
  data-ak-slide="attention"
  data-slide-container="attention"
  data-ak-width="1600"
  data-ak-height="900"
  data-ak-px-per-in="120"
>
  ...
</main>
```

Mark elements whose source geometry must be reused in PPTX:

```html
<h1 data-ak-measure="title">Attention 机制：结构与计算图</h1>
<section data-ak-measure="attention-panel">...</section>
<svg data-ak-measure="attention-svg" viewBox="0 0 1040 390">...</svg>
```

Use `data-ak-*` in new code. The reader also accepts legacy long names:

| Purpose | Preferred | Also accepted |
| :-- | :-- | :-- |
| Slide id | `data-ak-slide` | `data-artifact-kit-slide`, `data-slide-container` |
| Measured node id | `data-ak-measure` | `data-artifact-kit-measure` |
| Source slide width | `data-ak-width` | `data-artifact-kit-width`, `data-width` |
| Source slide height | `data-ak-height` | `data-artifact-kit-height`, `data-height` |
| Pixel-to-inch ratio | `data-ak-px-per-in` | `data-artifact-kit-px-per-in` |

## Runtime Output

After measurement, the runtime writes numeric values back to the DOM:

| Attribute | Meaning |
| :-- | :-- |
| `data-ak-x`, `data-ak-y` | Element top-left in source slide pixels |
| `data-ak-w`, `data-ak-h` | Element size in source slide pixels |
| `data-ak-in-x`, `data-ak-in-y` | Element top-left in PPTX inches |
| `data-ak-in-w`, `data-ak-in-h` | Element size in PPTX inches |
| `data-ak-font-pt` | Computed font size converted to PPT points |
| `data-ak-in-width`, `data-ak-in-height` | Slide size in PPTX inches |

The default conversion is:

```ts
const pptInches = sourcePx / pxPerIn;
const fontPt = (computedCssFontPx * 72) / pxPerIn;
```

For a 1600x900 HTML slide with `data-ak-px-per-in="120"`, the PPTX layout is `13.333 x 7.5`.

## Measurement Formula

The fallback runtime uses rendered browser geometry and compensates for CSS scale on the slide container:

```ts
const slideRect = slide.getBoundingClientRect();
const nodeRect = node.getBoundingClientRect();
const scaleX = slideRect.width / declaredSlideWidth;
const scaleY = slideRect.height / declaredSlideHeight;

const x = (nodeRect.left - slideRect.left) / scaleX;
const y = (nodeRect.top - slideRect.top) / scaleY;
const w = nodeRect.width / scaleX;
const h = nodeRect.height / scaleY;
```

This is accurate for normal rendered DOM. If a source workflow hides inactive pages with `display:none`, `visibility:hidden`, zero scale, offscreen transforms, or virtualization, provide a private runtime that clones/activates the page before measuring.

## Wrapper Usage

Use the measure helpers before building the deck:

```tsx
/** @jsxImportSource @artifact-kit/pptxgenjs-jsx */
import {
  Deck,
  Slide,
  Text,
  Rect,
  measureArtifacts,
  readFontPt,
  readPptBox,
  readSlideLayout,
  renderPptx,
} from "@artifact-kit/pptxgenjs-jsx";

await measureArtifacts();

const layout = readSlideLayout("attention");
const title = readPptBox("title");
const titleFont = readFontPt("title");

const deck = (
  <Deck layout={layout}>
    <Slide background={{ color: "FFFFFF" }}>
      <Text {...title} fontSize={titleFont} bold color="08265F">
        Attention 机制：结构与计算图
      </Text>
      <Rect {...readPptBox("attention-panel")} fill={{ color: "FFFFFF" }} line={{ color: "CBD5E1" }} />
    </Slide>
  </Deck>
);

await renderPptx(deck, { fileName: "attention.pptx" });
```

For inline browser JSX loaded from the IIFE build:

```js
const {
  Deck,
  Slide,
  Text,
  measureArtifacts,
  readPptBox,
  readSlideLayout,
  renderPptx,
} = window.ArtifactKitPptxGenJsx;
```

Do not read measured values at module parse time if the source DOM may still be loading. Put `await measureArtifacts()` and all `read*` calls inside the click handler or an async render function.

## Private Runtime Interface

A stronger runtime can be shipped privately and loaded before deck generation:

```ts
type ArtifactKitMeasure = {
  ready?: Promise<void> | (() => Promise<void> | void);
  measure?: () => Promise<void> | void;
  getBox?: (id: string) => {
    x?: number;
    y?: number;
    w?: number;
    h?: number;
    pxPerIn?: number;
    in?: { x?: number; y?: number; w?: number; h?: number };
  };
  getSlide?: (id?: string) => {
    width?: number;
    height?: number;
    pxPerIn?: number;
    in?: { width?: number; height?: number };
  };
  getValue?: (id: string, key: string) => number | string | undefined;
};

window.ArtifactKitMeasure = privateRuntime;
```

If this global exists and has `measure()`, `measureArtifacts()` delegates to it. If `getBox()` or `getSlide()` returns values, those values take precedence over DOM attributes.

## LLM Authoring Rules

1. Mark every reusable source block with `data-ak-measure="stable-id"`.
2. Mark the slide root with declared source pixel size and `data-ak-px-per-in`.
3. Read coordinates with `readPptBox(id)` instead of copying guessed numbers.
4. Express derived positions as formulas:

```ts
const svg = readPptBox("attention-svg");
const viewBox = { x: 0, y: 0, w: 1040, h: 390 };
const sx = svg.w / viewBox.w;
const sy = svg.h / viewBox.h;
const box = {
  x: svg.x + (174 - viewBox.x) * sx,
  y: svg.y + (54 - viewBox.y) * sy,
  w: 120 * sx,
  h: 48 * sy,
};
```

5. Use native PPTX objects where possible. Use screenshots only for visual details that cannot be represented editably.
