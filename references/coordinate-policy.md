# Coordinate Policy

The goal is not just visual similarity. The goal is an auditable conversion where every PPT coordinate has a defensible source.

## Allowed Coordinate Sources

Use these freely:

- `readPptBox(id)`, `readBox(id)`, `readSlideLayout(id)`, `readFontPt(id)`.
- Explicit HTML attributes, CSS rules, and Tailwind arbitrary values such as `w-[1600px]`.
- SVG source values: `viewBox`, `x`, `y`, `width`, `height`, `rx`, `d`, line endpoints, text anchors.
- Declared conversion constants such as `data-ak-px-per-in="120"` and `const inch = (px) => px / 120`.
- Data values from charts, tables, or source JavaScript arrays.

Use sparingly and explain in nearby code:

- Internal label insets inside a measured shape, such as `box.x + box.w * 0.08`.
- Text-box height ratios used only to center a label inside a source SVG rectangle.
- Simplified chart axis/tick sizing when using native PPT charts instead of recreating every SVG tick.

## Disallowed Coordinate Sources

Do not use:

- Visual guessing from screenshots.
- Handwritten `x/y/w/h` for DOM elements that could be marked and measured.
- Final inch coordinates without showing the source pixel value or measured box.
- Negative line widths/heights to represent SVG endpoints. Use `LineBetween`.
- Layout constants copied from a previous output after the source DOM changed.

## Expected Code Shape

Good DOM-derived placement:

```tsx
<Text {...readPptBox("subtitle")} fontSize={readFontPt("subtitle")} italic margin={0}>
  {text("[data-ak-measure='subtitle']")}
</Text>
```

Good SVG-derived placement:

```ts
const svg = readPptBox("flow-svg");
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

Bad placement:

```tsx
<Text x={0.72} y={0.48} w={6.1} h={0.3}>Title</Text>
```

This is only acceptable if the source itself is already expressed in PPT inches.

## Reviewing Existing Code

Search for these patterns:

```text
x: inch(
y: inch(
w: inch(
h: inch(
at(
pptBox({
```

Every match must be one of:

- A measured box helper call.
- A conversion of explicit source HTML/CSS/SVG values.
- SVG viewBox mapping.
- A small local label inset inside an already measured/SVG-derived object.

If a match exists because "it looked right", replace it with a marker and `readPptBox`.
