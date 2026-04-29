---
name: html-to-pptx-jsx
description: Create downloadable, editable PowerPoint decks from HTML pages by copying the source into an exporter page, marking measured DOM nodes, and writing inline browser JSX with @artifact-kit/pptxgenjs-jsx. Use for local HTML files, generated web pages, dashboards, reports, slide-like Tailwind pages, SVG-heavy pages, or any workflow that needs HTML-to-PPTX reconstruction with DOM measurement rather than guessed coordinates.
---

# HTML to PPTX JSX

Use `@artifact-kit/pptxgenjs-jsx` to turn rendered HTML into an editable PowerPoint deck. The default workflow is measure-first: preserve the original input, create a separate exporter HTML, mark the exporter DOM with `data-ak-*` measurement attributes, then build a JSX `<Deck>` from measured boxes and source SVG primitives.

## Required Stage Gates

Do not jump directly from input HTML to a finished exporter. Before writing the final `output.html` or exporter code, produce these intermediate artifacts in your working notes, response, or as a top-of-file comment in the generated exporter:

1. **File plan**: input path, exporter path, confirmation that the input remains read-only.
2. **Slide decomposition**: component tree from large to small, such as `Deck -> Slide -> Header -> MainGrid -> Panel -> Diagram`.
3. **Measurement manifest**: every required `data-ak-measure` id, the DOM selector it marks, and why the PPT needs its box.
4. **SVG inventory**: every source `<svg>`, its `viewBox`, important primitives (`rect`, `line`, `path`, `circle`, `text`, chart marks), and a mapping decision for each group.
5. **Fallback list**: any raster/image fallback with a specific reason. Empty is preferred.

If any SVG has readable primitives, do not embed that SVG as a PNG. Map its primitives into editable PPT shapes unless the fallback list documents why native reconstruction is impossible.

## Core Workflow

1. Treat the original input HTML as read-only. Do not add `data-ak-*`, buttons, scripts, or generated code to it.
2. Copy the input into a generated exporter HTML. Add the export button, `@artifact-kit/pptxgenjs-jsx` browser IIFE, Babel Standalone, and measurement markers only to the exporter.
3. Complete the required stage gates above. Do not continue until the decomposition, measurement manifest, and SVG inventory exist.
4. Mark the slide root with `data-ak-slide`, `data-ak-width`, `data-ak-height`, and `data-ak-px-per-in`.
5. Mark every DOM block, text node, SVG, chart region, footer item, and repeated card that will become PPT content with `data-ak-measure="stable-id"`.
6. In the export button handler, call `await measureArtifacts({ document })`, then read positions with `readPptBox(id)`, `readFontPt(id)`, and `readSlideLayout(id)`.
7. Author a componentized JSX `<Deck>` using native PPT objects. Use `Text`, `TextRun`, shape components, `LineBetween`, `CustomGeometry`, tables, images, and native chart components.
8. Run `validateDeck(deck)`, call `renderPptx(deck, { fileName })`, open the downloaded deck, and visually compare it against the exporter page.

Start from [assets/browser-inline-jsx-template.html](assets/browser-inline-jsx-template.html) when creating a fresh exporter.

## Non-Negotiable Rules

- Never place DOM-derived elements by visual guesswork.
- Never create only a final `output.html` without first creating or embedding the stage-gate artifacts.
- If an element is rendered DOM, measure it with `data-ak-measure` and `readPptBox`.
- If an element is inside SVG, map it from the SVG source `viewBox` and primitive coordinates.
- If neither DOM measurement nor source geometry is available, explicitly choose an image/snapdom fallback and document why editability is not practical.
- Do not rasterize SVGs just because native mapping takes more work.
- Keep arithmetic visible in generated JS. Agents should be able to audit why every coordinate exists.
- Split the generated JSX into named components. Avoid one monolithic slide function.
- Prefer native editable PPT objects over screenshots. Use raster fallback only for details that cannot be represented editably.
- Use browser inline JSX only for local authoring or agent workflows. For shipped apps, precompile with Vite or another build tool.
- Skill examples should use the unversioned CDN URL, or at most a major-version URL if the CDN supports it, so wrapper bugfixes are picked up. Pin exact versions only for archived deliverables after testing.

## What To Read

Always read:

1. [references/measure-first-workflow.md](references/measure-first-workflow.md)
2. [references/coordinate-policy.md](references/coordinate-policy.md)
3. [references/one-shot-agent-contract.md](references/one-shot-agent-contract.md)
4. [references/pptxgenjs-jsx-llms.txt](references/pptxgenjs-jsx-llms.txt)
5. [references/pptxgenjs-jsx-quickstart.md](references/pptxgenjs-jsx-quickstart.md)

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
