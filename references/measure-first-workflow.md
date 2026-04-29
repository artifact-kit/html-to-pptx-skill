# Measure-First Workflow

Use this workflow whenever the source is HTML or a browser-rendered page.

## 1. Preserve The Input

Keep the original input file clean. Do not add export buttons, scripts, `data-ak-*`, generated constants, or comments to it.

Create a separate exporter:

```text
examples/input/source.html              # clean input
examples/generated/source-export.html   # measured exporter
```

The exporter can be a copy of the input with an added toolbar, measurement markers, and inline JSX.

## 2. Load Runtime Before Babel

```html
<script src="https://unpkg.com/@artifact-kit/pptxgenjs-jsx/dist/pptxgenjs-jsx.browser.iife.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

Use the unversioned CDN URL in skill examples so wrapper bugfixes are picked up. Pin a tested version only for archived or production workflows.

## 3. Mark The Exporter DOM

Mark the slide root:

```html
<main
  data-ak-slide="slide"
  data-ak-width="1600"
  data-ak-height="900"
  data-ak-px-per-in="120"
>
  ...
</main>
```

Mark anything whose box will be reused:

```html
<h1 data-ak-measure="title">...</h1>
<section data-ak-measure="main-panel">...</section>
<svg data-ak-measure="flow-svg" viewBox="0 0 1040 390">...</svg>
<p data-ak-measure="footer-copy">...</p>
```

Mark both containers and children when both matter. A panel box, its title text, its SVG, and its caption should usually each have their own marker.

## 4. Measure Inside The Click Handler

Do not read measurement values at module parse time. The DOM, fonts, and layout may still be settling.

```tsx
button.addEventListener("click", async () => {
  await measureArtifacts({ document });

  const layout = readSlideLayout("slide");
  const title = readPptBox("title");
  const titlePt = readFontPt("title");
  // Build deck here.
});
```

## 5. Build Native PPT Objects

Use the measured values directly:

```tsx
<Text {...readPptBox("title")} fontSize={readFontPt("title")} bold margin={0}>
  {text("[data-ak-measure='title']")}
</Text>

<RoundRect
  {...readPptBox("main-panel")}
  rectRadius={0.025}
  fill={{ color: "FFFFFF", transparency: 8 }}
  line={{ color: "CBD5E1", width: 0.8 }}
/>
```

For SVG contents, measure the SVG element once, then map primitives from the SVG viewBox. See [svg-viewbox-mapping.md](svg-viewbox-mapping.md).

## 6. Validate And Download

```tsx
const issues = validateDeck(deck);
if (issues.some((issue) => issue.level === "error")) {
  status.textContent = JSON.stringify(issues, null, 2);
  return;
}

await renderPptx(deck, { fileName: "deck.pptx" });
```

After download, open the deck and compare:

- Outer panel positions and sizes.
- Text positions and font sizes.
- SVG arrow directions.
- Chart sizes, legends, labels, and plot area.
- Whether native objects are selectable/editable.
