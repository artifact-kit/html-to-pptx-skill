# Native Reconstruction Patterns

Use this before writing JSX for non-trivial pages. The goal is to stop text-only or invented-API output.

## API Legality Gate

Before using any component or prop, confirm it exists in one of:

- `references/pptxgenjs-jsx-component-manifest.json`
- `references/pptxgenjs-jsx-component-selection.md`
- `references/pptxgenjs-jsx-common-props.md`
- `references/pptxgenjs-jsx-shape-props.md`
- `references/pptxgenjs-jsx-chart-props.md`

Do not invent components, chart types, or props.

Invalid:

```tsx
<Chart type="heatmap" lineSize="small" />
```

Why invalid:

- `heatmap` is not a valid `CHART_NAME`.
- `lineSize` is a number in points, not `"small"`.
- Use dedicated chart components such as `LineChart` when available.

## Visual Component Choices

| Source visual | Preferred PPT JSX |
| :-- | :-- |
| paragraph, heading, label | `Text`, `TextRun` |
| card or panel background | `RoundRect` or `Rect` plus child `Text` |
| pill/badge | `RoundRect` plus `Text` |
| avatar/dot/marker | `Ellipse` |
| divider/rule | `Line` |
| endpoint arrow, diagonal arrow, vertical arrow | `LineBetween` |
| SVG rectangle | `Rect` or `RoundRect` from viewBox mapping |
| SVG line/path arrow | `LineBetween` from mapped endpoints |
| SVG polygon/path blob | `CustomGeometry` |
| heatmap/matrix | `Rect` grid or `Table`; not `Chart type="heatmap"` |
| line chart with data | `LineChart` |
| bar/column chart with data | `BarChart` |
| unsupported chart with recoverable marks | reconstruct with shapes, or use nearest native chart only if semantically correct |

If the page contains shapes, the PPT must contain shapes. A text-only reconstruction is incomplete unless the source is text-only.

## Heatmap Or Matrix Pattern

PowerPoint/PptxGenJS does not expose a native heatmap chart type. Build a heatmap as editable cells.

```tsx
function NativeHeatmap({ box, values }) {
  const rows = values.length;
  const cols = values[0].length;
  const cellW = box.w / cols;
  const cellH = box.h / rows;

  return (
    <Fragment>
      {values.map((row, r) =>
        row.map((value, c) => (
          <Rect
            x={box.x + c * cellW}
            y={box.y + r * cellH}
            w={cellW}
            h={cellH}
            fill={{ color: colorScale(value) }}
            line={{ color: "FFFFFF", width: 0.2 }}
          />
        ))
      )}
      <Rect {...box} fill={{ color: "FFFFFF", transparency: 100 }} line={{ color: "334155", width: 0.7 }} />
    </Fragment>
  );
}
```

If the heatmap is inside SVG, measure the SVG element, map the SVG heatmap rect from `viewBox`, then pass that mapped box to `NativeHeatmap`.

## Native Line Chart Pattern

Use `LineChart`, not generic `Chart`, when the source is a line chart and the data is recoverable.

```tsx
<LineChart
  {...readPptBox("chart-svg")}
  data={[
    { name: "standard", labels: ["16", "64", "256", "1k"], values: [3, 9, 26, 48] },
    { name: "linear", labels: ["16", "64", "256", "1k"], values: [12, 17, 24, 31] },
  ]}
  showLegend
  legendPos="t"
  showTitle={false}
  showValue={false}
  chartColors={["2563EB", "F97316"]}
  lineSize={1.5}
  markerSize={3}
/>
```

Use numeric chart props from `pptxgenjs-jsx-chart-props.md`. Do not use invented tokens such as `lineSize="small"`.

## LineBetween Pattern

`LineBetween` requires numeric endpoint props in PPT inches.

Good:

```tsx
const a = viewBoxPoint(svgBox, viewBox, { x: 120, y: 80 });
const b = viewBoxPoint(svgBox, viewBox, { x: 180, y: 140 });

<LineBetween
  x1={a.x}
  y1={a.y}
  x2={b.x}
  y2={b.y}
  line={{ color: "08265F", width: 1.1, endArrowType: "triangle" }}
/>
```

Bad:

```tsx
<LineBetween {...readPptBox("arrow")} />
<LineBetween {...rmatrix({ x: 0, y: 0, w: 360, h: 218 })} />
```

A box has `x/y/w/h`; a line endpoint needs `x1/y1/x2/y2`.

## Shape Inventory Pattern

For each major region, write a mini inventory before coding:

```text
region: hero-card
source visuals:
- rounded card background -> RoundRect
- eyebrow text -> Text
- metric badges -> RoundRect + Text
- diagonal connector -> LineBetween
- decorative star -> Star or Shape shape="star5"
required components: RoundRect, Text, LineBetween, Star
props docs checked: common-props, shape-props
```

Then implement named components:

```tsx
function HeroCard({ box }) {
  return (
    <Fragment>
      <RoundRect {...box} rectRadius={0.04} fill={{ color: "FFFFFF" }} line={{ color: "CBD5E1", width: 0.8 }} />
      <Text {...readPptBox("hero-title")} fontSize={readFontPt("hero-title")} bold margin={0}>
        {text("hero-title")}
      </Text>
    </Fragment>
  );
}
```

## Complex Example

For a full example with measured DOM, native shape reconstruction, SVG viewBox mapping, a heatmap built from editable `Rect` cells, and a native `LineChart`, inspect:

```text
assets/complex-native-exporter-example.html
```

