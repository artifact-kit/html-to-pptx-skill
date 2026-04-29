# LLM Quickstart

This is the default context agents should read before writing code with `@artifact-kit/pptxgenjs-jsx`.

## Core Rules

1. Use TSX with `/** @jsxImportSource @artifact-kit/pptxgenjs-jsx */`.
2. Prefer dedicated components: `RoundRect`, `BarChart`, `TableCell`, etc.
3. Use PptxGenJS prop names exactly: `x`, `y`, `w`, `h`, `fill`, `line`, `fontFace`, `fontSize`, `chartColors`.
4. Coordinates are PptxGenJS inches or percentages, not CSS pixels.
5. Use hex colors without `#`.
6. Run `validateDeck(deck)` before `renderPptx(deck)`.
7. Use `Shape`, `Chart`, or `Raw` as escape hatches when dedicated components do not cover an upstream feature.

## Common Components

- `Deck`: Root presentation.
- `Presentation`: Readable alias for Deck.
- `Slide`: Create a slide.
- `Layout`: Define an additional custom layout.
- `Section`: Group nested slides into a PowerPoint section.
- `Master`: Define a reusable slide master.
- `Placeholder`: Add a placeholder inside Master.
- `Text`: Text box, rich text container, or text inside a shape.
- `TextRun`: Per-run formatting inside Text.
- `Notes`: Speaker notes.
- `Image`: Image by path or data URI/base64.
- `Media`: Audio, video, or online media.
- `Table`: PowerPoint table.
- `TableRow`: Declarative row inside Table.
- `TableCell`: Declarative cell inside TableRow.
- `TableToSlides`: Convert an HTML table in browser/runtime DOM.

## Basic TSX Example

```tsx
/** @jsxImportSource @artifact-kit/pptxgenjs-jsx */
import { Deck, Slide, Text, RoundRect, validateDeck, renderPptx } from "@artifact-kit/pptxgenjs-jsx";

const deck = (
  <Deck title="Example" layout={{ name: "WIDE", width: 13.333, height: 7.5 }}>
    <Slide background={{ color: "FFFFFF" }}>
      <RoundRect x={1} y={1} w={4} h={0.8} rectRadius={0.08} fill={{ color: "EEF2FF" }} />
      <Text x={1.2} y={1.22} w={3.5} h={0.35} fontSize={18} color="111827" bold>Hello PPTX</Text>
    </Slide>
  </Deck>
);

const issues = validateDeck(deck);
if (issues.some((issue) => issue.level === "error")) throw new Error(JSON.stringify(issues, null, 2));
await renderPptx(deck, { fileName: "example.pptx" });
```

## Browser JSX With Babel Standalone

For local workflows, HTML can import Babel Standalone and write JSX directly. Use Babel's classic JSX runtime with `/** @jsx h */`, then import `h` from this package. See `examples/browser-jsx.html`.

## No JSX Transform

```ts
import { Deck, Slide, Text, h, renderPptx } from "@artifact-kit/pptxgenjs-jsx";

const deck = h(Deck, { title: "No JSX" },
  h(Slide, { background: { color: "FFFFFF" } },
    h(Text, { text: "Hello", x: 1, y: 1, w: 4, h: 0.5 })
  )
);

await renderPptx(deck, { fileName: "no-jsx.pptx" });
```
