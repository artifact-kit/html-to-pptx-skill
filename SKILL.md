---
name: html-to-pptx-jsx
description: Create downloadable, editable PowerPoint decks from HTML pages by copying the source into an exporter page, marking measured DOM nodes, and writing inline browser JSX with @artifact-kit/pptxgenjs-jsx. Use for local HTML files, generated web pages, dashboards, reports, slide-like Tailwind pages, SVG-heavy pages, or any workflow that needs HTML-to-PPTX reconstruction with DOM measurement rather than guessed coordinates.
---

# HTML to PPTX JSX

Use `@artifact-kit/pptxgenjs-jsx` to turn rendered HTML into an editable PowerPoint deck. The default workflow is measure-first: preserve the original input, create a separate exporter HTML, mark the exporter DOM with `data-ak-*` measurement attributes, then build a JSX `<Deck>` from measured boxes and source SVG primitives.

## Core Workflow

1. Treat the original input HTML as read-only. Do not add `data-ak-*`, buttons, scripts, or generated code to it.
2. Copy the input into a generated exporter HTML. Add the export button, `@artifact-kit/pptxgenjs-jsx` browser IIFE, Babel Standalone, and measurement markers only to the exporter.
3. Mark the slide root with `data-ak-slide`, `data-ak-width`, `data-ak-height`, and `data-ak-px-per-in`.
4. Mark every DOM block, text node, SVG, chart region, footer item, and repeated card that will become PPT content with `data-ak-measure="stable-id"`.
5. In the export button handler, call `await measureArtifacts({ document })`, then read positions with `readPptBox(id)`, `readFontPt(id)`, and `readSlideLayout(id)`.
6. Author a JSX `<Deck>` using native PPT objects. Use `Text`, `TextRun`, shape components, `LineBetween`, `CustomGeometry`, tables, images, and native chart components.
7. Run `validateDeck(deck)`, call `renderPptx(deck, { fileName })`, open the downloaded deck, and visually compare it against the exporter page.

Start from [assets/browser-inline-jsx-template.html](assets/browser-inline-jsx-template.html) when creating a fresh exporter.

## Non-Negotiable Rules

- Never place DOM-derived elements by visual guesswork.
- If an element is rendered DOM, measure it with `data-ak-measure` and `readPptBox`.
- If an element is inside SVG, map it from the SVG source `viewBox` and primitive coordinates.
- If neither DOM measurement nor source geometry is available, explicitly choose an image/snapdom fallback and document why editability is not practical.
- Keep arithmetic visible in generated JS. Agents should be able to audit why every coordinate exists.
- Prefer native editable PPT objects over screenshots. Use raster fallback only for details that cannot be represented editably.
- Use browser inline JSX only for local authoring or agent workflows. For shipped apps, precompile with Vite or another build tool.
- Skill examples should use the unversioned CDN URL, or at most a major-version URL if the CDN supports it, so wrapper bugfixes are picked up. Pin exact versions only for archived deliverables after testing.

## What To Read

Always read:

1. [references/measure-first-workflow.md](references/measure-first-workflow.md)
2. [references/coordinate-policy.md](references/coordinate-policy.md)
3. [references/pptxgenjs-jsx-llms.txt](references/pptxgenjs-jsx-llms.txt)
4. [references/pptxgenjs-jsx-quickstart.md](references/pptxgenjs-jsx-quickstart.md)

Read when needed:

- SVG-heavy pages: [references/svg-viewbox-mapping.md](references/svg-viewbox-mapping.md)
- Final checks: [references/audit-checklist.md](references/audit-checklist.md)
- Broader heuristics: [references/html-recreation-guide.md](references/html-recreation-guide.md)
- Wrapper measure API details: [references/pptxgenjs-jsx-measure-contract.md](references/pptxgenjs-jsx-measure-contract.md)
- Component choice: [references/pptxgenjs-jsx-component-selection.md](references/pptxgenjs-jsx-component-selection.md)
- Common props: [references/pptxgenjs-jsx-common-props.md](references/pptxgenjs-jsx-common-props.md)
- Shape props: [references/pptxgenjs-jsx-shape-props.md](references/pptxgenjs-jsx-shape-props.md)
- Chart props: [references/pptxgenjs-jsx-chart-props.md](references/pptxgenjs-jsx-chart-props.md)
- Full upstream surface: [references/pptxgenjs-jsx-all-upstream-props.md](references/pptxgenjs-jsx-all-upstream-props.md)
- Machine-readable component list: [references/pptxgenjs-jsx-component-manifest.json](references/pptxgenjs-jsx-component-manifest.json)

If `node_modules/@artifact-kit/pptxgenjs-jsx` exists and may be newer than this skill, prefer its `llms.txt`, `docs/`, and `component-manifest.json` after reading this workflow.

## Browser Inline JSX Pattern

Use classic JSX with Babel Standalone:

```tsx
/** @jsx pptxElement */
const {
  Deck,
  Slide,
  Text,
  measureArtifacts,
  pptxElement,
  readFontPt,
  readPptBox,
  readSlideLayout,
  renderPptx,
  validateDeck,
} = window.ArtifactKitPptxGenJsx;

document.querySelector("#export").addEventListener("click", async () => {
  await measureArtifacts({ document });

  const layout = readSlideLayout("slide");
  const title = readPptBox("title");
  const deck = (
    <Deck title="Measured deck" layout={layout}>
      <Slide background={{ color: "FFFFFF" }}>
        <Text {...title} fontSize={readFontPt("title")} bold margin={0}>
          {document.querySelector('[data-ak-measure="title"]').textContent.trim()}
        </Text>
      </Slide>
    </Deck>
  );

  const issues = validateDeck(deck);
  if (issues.some((issue) => issue.level === "error")) throw new Error(JSON.stringify(issues, null, 2));
  await renderPptx(deck, { fileName: "measured-deck.pptx" });
});
```

Do not use `@jsxImportSource` in inline Babel unless the React preset is explicitly configured for automatic runtime. The default is `/** @jsx pptxElement */`.
