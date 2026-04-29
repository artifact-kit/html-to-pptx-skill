# SVG ViewBox Mapping

Use this when a measured DOM element is an SVG and its contents should become editable PPT shapes.

## Base Formula

Measure the SVG element:

```ts
const svg = readPptBox("flow-svg");
const viewBox = { x: 0, y: 0, w: 1040, h: 390 };

const point = (p) => ({
  x: svg.x + ((p.x - viewBox.x) / viewBox.w) * svg.w,
  y: svg.y + ((p.y - viewBox.y) / viewBox.h) * svg.h,
});

const rect = (r) => {
  const p = point(r);
  return {
    x: p.x,
    y: p.y,
    w: (r.w / viewBox.w) * svg.w,
    h: (r.h / viewBox.h) * svg.h,
  };
};
```

The numbers in `point()` and `rect()` must come from the SVG source, not from visual estimation.

## Primitive Mapping

| SVG source | PPTX JSX |
| :-- | :-- |
| `<rect x y width height rx>` | `RoundRect` or `Rect` with `rect({...})` |
| `<line x1 y1 x2 y2>` | `LineBetween` using `point({x:x1,y:y1})` and `point({x:x2,y:y2})` |
| `path d="M x1 y1 L x2 y2"` | `LineBetween` if it is a simple line |
| `<circle cx cy r>` | `Ellipse` with mapped `cx-r`, `cy-r`, `2r`, `2r` |
| `<ellipse cx cy rx ry>` | `Ellipse` with mapped `cx-rx`, `cy-ry`, `2rx`, `2ry` |
| `<text x y>` | `Text` with mapped anchor and source font size scaled from SVG to PPT |
| Complex `<path>` | `CustomGeometry` with local points |

## Lines And Arrows

Always use `LineBetween` for SVG endpoints:

```tsx
const a = point({ x: 135, y: 142 });
const b = point({ x: 170, y: 80 });

<LineBetween
  x1={a.x}
  y1={a.y}
  x2={b.x}
  y2={b.y}
  line={{ color: "08265F", width: 1.2, endArrowType: "triangle" }}
/>
```

Do not use raw `Line` with `w = x2 - x1` and `h = y2 - y1`; PowerPoint lines use a shape box model and can reverse arrows when the slope is negative or vertical.

## Custom Geometry

For path shapes, compute the path bounding box in SVG units, map that bbox to PPT inches, then convert each path point to local PPT units relative to the bbox.

```tsx
const bbox = { x: 120, y: 40, w: 56, h: 36 };
const local = (x, y) => ({
  x: ((x - bbox.x) / viewBox.w) * svg.w,
  y: ((y - bbox.y) / viewBox.h) * svg.h,
});

<CustomGeometry
  {...rect(bbox)}
  points={[
    { ...local(120, 40), moveTo: true },
    local(160, 40),
    local(176, 58),
    local(160, 76),
    local(120, 76),
    { close: true },
  ]}
  fill={{ color: "08265F" }}
  line={{ color: "08265F", transparency: 100 }}
/>
```

## Native Charts From SVG Charts

If the source chart is SVG but data is recoverable, prefer native PPT charts. Measure the full chart SVG or plot panel, then use that measured box for the native chart.

Exact SVG tick positions are less important than:

- Editable chart data.
- Similar chart box size.
- Similar series colors.
- Comparable legend position.
- Readable axis labels.

Use image fallback only when chart semantics or data are unavailable.
