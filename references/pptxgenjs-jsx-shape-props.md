# Shape Props

Use dedicated shape components when available. Use `<Shape shape="VALUE" ... />` for every other PptxGenJS shape.

## Dedicated Shape Components

- `Rect`
- `RoundRect`
- `Ellipse` / `Oval`
- `Line`
- `Arc`
- `BlockArc`
- `PieShape`
- `CustomGeometry`
- `Triangle`
- `RightTriangle`
- `Diamond`
- `Pentagon`
- `Hexagon`
- `Star`, `Star4`, `Star5`, `Star6`, `Star8`, `Star10`
- `LeftArrow`, `RightArrow`, `UpArrow`, `DownArrow`, `LeftRightArrow`, `UpDownArrow`
- `Chevron`, `Cloud`, `Heart`, `Donut`, `Plus`

## Wrapper-Specific Shape Props

### `RoundRectProps`

Extends: `ShapeProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `rectRadius?` | `number` | Rounded rectangle radius. Valid only for `roundRect`; range 0.0 to 1.0. |

### `ArcProps`

Extends: `ShapeProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `angleRange?` | `[number, number]` | Arc angle range. Valid for `arc`, `pie`, and `blockArc`; range [0-359, 0-359]. |

### `BlockArcProps`

Extends: `ArcProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `arcThicknessRatio?` | `number` | Block arc thickness ratio. Valid only for `blockArc`; range 0.0 to 1.0. |

### `CustomGeometryProps`

Extends: `ShapeProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `points` | `CustomGeometryPoint[]` | Required custom geometry path points passed to PptxGenJS `custGeom`. Coordinates are local PPT units inside the custom geometry box, not raw SVG units. |

```ts
type CustomGeometryPoint =
  | { x: Coord; y: Coord; moveTo?: boolean }
  | { x: Coord; y: Coord; curve: { type: "cubic"; x1: Coord; y1: Coord; x2: Coord; y2: Coord } }
  | { x: Coord; y: Coord; curve: { type: "quadratic"; x1: Coord; y1: Coord } }
  | { x: Coord; y: Coord; curve: { type: "arc"; hR: Coord; wR: Coord; stAng: number; swAng: number } }
  | { close: true };
```

SVG conversion rule:

1. Compute the source SVG element's absolute pixel box from DOM/CSS/source attributes.
2. Convert the path bounding box to slide PPT inches with formulas: `x = inch(svgLeftPx + pathBBox.x * svgScaleX)`, `y = inch(svgTopPx + pathBBox.y * svgScaleY)`, `w = inch(pathBBox.width * svgScaleX)`, `h = inch(pathBBox.height * svgScaleY)`.
3. Convert path coordinates into local PPT inches by subtracting the path bbox origin, applying the SVG render scale, then applying `inch(...)`. For example SVG `M 140 40 L 180 60` with `pathBBox.x = 120`, `pathBBox.y = 30`, `svgScaleX = 0.5`, and `svgScaleY = 0.5` becomes `[{ x: inch(20 * 0.5), y: inch(10 * 0.5), moveTo: true }, { x: inch(60 * 0.5), y: inch(30 * 0.5) }]`.
4. Map SVG commands: `M` -> `moveTo`, `L/H/V` -> line points, `C` -> cubic curve, `Q` -> quadratic curve, `Z` -> `{ close: true }`. Use native `Line`, `Rect`, `Ellipse`, and arrow shapes for simpler primitives.

## Shape Type Alias

### `SHAPE_NAME`

```ts
type SHAPE_NAME = |'accentBorderCallout1'|'accentBorderCallout2'|'accentBorderCallout3'|'accentCallout1'|'accentCallout2'|'accentCallout3'|'actionButtonBackPrevious'|'actionButtonBeginning'|'actionButtonBlank'|'actionButtonDocument'|'actionButtonEnd'|'actionButtonForwardNext'|'actionButtonHelp'|'actionButtonHome'|'actionButtonInformation'|'actionButtonMovie'|'actionButtonReturn'|'actionButtonSound'|'arc'|'bentArrow'|'bentUpArrow'|'bevel'|'blockArc'|'borderCallout1'|'borderCallout2'|'borderCallout3'|'bracePair'|'bracketPair'|'callout1'|'callout2'|'callout3'|'can'|'chartPlus'|'chartStar'|'chartX'|'chevron'|'chord'|'circularArrow'|'cloud'|'cloudCallout'|'corner'|'cornerTabs'|'cube'|'curvedDownArrow'|'curvedLeftArrow'|'curvedRightArrow'|'curvedUpArrow'|'decagon'|'diagStripe'|'diamond'|'dodecagon'|'donut'|'doubleWave'|'downArrow'|'downArrowCallout'|'ellipse'|'ellipseRibbon'|'ellipseRibbon2'|'flowChartAlternateProcess'|'flowChartCollate'|'flowChartConnector'|'flowChartDecision'|'flowChartDelay'|'flowChartDisplay'|'flowChartDocument'|'flowChartExtract'|'flowChartInputOutput'|'flowChartInternalStorage'|'flowChartMagneticDisk'|'flowChartMagneticDrum'|'flowChartMagneticTape'|'flowChartManualInput'|'flowChartManualOperation'|'flowChartMerge'|'flowChartMultidocument'|'flowChartOfflineStorage'|'flowChartOffpageConnector'|'flowChartOnlineStorage'|'flowChartOr'|'flowChartPredefinedProcess'|'flowChartPreparation'|'flowChartProcess'|'flowChartPunchedCard'|'flowChartPunchedTape'|'flowChartSort'|'flowChartSummingJunction'|'flowChartTerminator'|'folderCorner'|'frame'|'funnel'|'gear6'|'gear9'|'halfFrame'|'heart'|'heptagon'|'hexagon'|'homePlate'|'horizontalScroll'|'irregularSeal1'|'irregularSeal2'|'leftArrow'|'leftArrowCallout'|'leftBrace'|'leftBracket'|'leftCircularArrow'|'leftRightArrow'|'leftRightArrowCallout'|'leftRightCircularArrow'|'leftRightRibbon'|'leftRightUpArrow'|'leftUpArrow'|'lightningBolt'|'line'|'lineInv'|'mathDivide'|'mathEqual'|'mathMinus'|'mathMultiply'|'mathNotEqual'|'mathPlus'|'moon'|'noSmoking'|'nonIsoscelesTrapezoid'|'notchedRightArrow'|'octagon'|'parallelogram'|'pentagon'|'pie'|'pieWedge'|'plaque'|'plaqueTabs'|'plus'|'quadArrow'|'quadArrowCallout'|'rect'|'ribbon'|'ribbon2'|'rightArrow'|'rightArrowCallout'|'rightBrace'|'rightBracket'|'round1Rect'|'round2DiagRect'|'round2SameRect'|'roundRect'|'rtTriangle'|'smileyFace'|'snip1Rect'|'snip2DiagRect'|'snip2SameRect'|'snipRoundRect'|'squareTabs'|'star10'|'star12'|'star16'|'star24'|'star32'|'star4'|'star5'|'star6'|'star7'|'star8'|'stripedRightArrow'|'sun'|'swooshArrow'|'teardrop'|'trapezoid'|'triangle'|'upArrow'|'upArrowCallout'|'upDownArrow'|'upDownArrowCallout'|'uturnArrow'|'verticalScroll'|'wave'|'wedgeEllipseCallout'|'wedgeRectCallout'|'wedgeRoundRectCallout'
```

## Full Shape List

| Shape values |
| :-- |
| `accentBorderCallout1` | `accentBorderCallout2` | `accentBorderCallout3` | `accentCallout1` |
| `accentCallout2` | `accentCallout3` | `actionButtonBackPrevious` | `actionButtonBeginning` |
| `actionButtonBlank` | `actionButtonDocument` | `actionButtonEnd` | `actionButtonForwardNext` |
| `actionButtonHelp` | `actionButtonHome` | `actionButtonInformation` | `actionButtonMovie` |
| `actionButtonReturn` | `actionButtonSound` | `arc` | `bentArrow` |
| `bentUpArrow` | `bevel` | `blockArc` | `borderCallout1` |
| `borderCallout2` | `borderCallout3` | `bracePair` | `bracketPair` |
| `callout1` | `callout2` | `callout3` | `can` |
| `chartPlus` | `chartStar` | `chartX` | `chevron` |
| `chord` | `circularArrow` | `cloud` | `cloudCallout` |
| `corner` | `cornerTabs` | `cube` | `curvedDownArrow` |
| `curvedLeftArrow` | `curvedRightArrow` | `curvedUpArrow` | `decagon` |
| `diagStripe` | `diamond` | `dodecagon` | `donut` |
| `doubleWave` | `downArrow` | `downArrowCallout` | `ellipse` |
| `ellipseRibbon` | `ellipseRibbon2` | `flowChartAlternateProcess` | `flowChartCollate` |
| `flowChartConnector` | `flowChartDecision` | `flowChartDelay` | `flowChartDisplay` |
| `flowChartDocument` | `flowChartExtract` | `flowChartInputOutput` | `flowChartInternalStorage` |
| `flowChartMagneticDisk` | `flowChartMagneticDrum` | `flowChartMagneticTape` | `flowChartManualInput` |
| `flowChartManualOperation` | `flowChartMerge` | `flowChartMultidocument` | `flowChartOfflineStorage` |
| `flowChartOffpageConnector` | `flowChartOnlineStorage` | `flowChartOr` | `flowChartPredefinedProcess` |
| `flowChartPreparation` | `flowChartProcess` | `flowChartPunchedCard` | `flowChartPunchedTape` |
| `flowChartSort` | `flowChartSummingJunction` | `flowChartTerminator` | `folderCorner` |
| `frame` | `funnel` | `gear6` | `gear9` |
| `halfFrame` | `heart` | `heptagon` | `hexagon` |
| `homePlate` | `horizontalScroll` | `irregularSeal1` | `irregularSeal2` |
| `leftArrow` | `leftArrowCallout` | `leftBrace` | `leftBracket` |
| `leftCircularArrow` | `leftRightArrow` | `leftRightArrowCallout` | `leftRightCircularArrow` |
| `leftRightRibbon` | `leftRightUpArrow` | `leftUpArrow` | `lightningBolt` |
| `line` | `lineInv` | `mathDivide` | `mathEqual` |
| `mathMinus` | `mathMultiply` | `mathNotEqual` | `mathPlus` |
| `moon` | `noSmoking` | `nonIsoscelesTrapezoid` | `notchedRightArrow` |
| `octagon` | `parallelogram` | `pentagon` | `pie` |
| `pieWedge` | `plaque` | `plaqueTabs` | `plus` |
| `quadArrow` | `quadArrowCallout` | `rect` | `ribbon` |
| `ribbon2` | `rightArrow` | `rightArrowCallout` | `rightBrace` |
| `rightBracket` | `round1Rect` | `round2DiagRect` | `round2SameRect` |
| `roundRect` | `rtTriangle` | `smileyFace` | `snip1Rect` |
| `snip2DiagRect` | `snip2SameRect` | `snipRoundRect` | `squareTabs` |
| `star10` | `star12` | `star16` | `star24` |
| `star32` | `star4` | `star5` | `star6` |
| `star7` | `star8` | `stripedRightArrow` | `sun` |
| `swooshArrow` | `teardrop` | `trapezoid` | `triangle` |
| `upArrow` | `upArrowCallout` | `upDownArrow` | `upDownArrowCallout` |
| `uturnArrow` | `verticalScroll` | `wave` | `wedgeEllipseCallout` |
| `wedgeRectCallout` | `wedgeRoundRectCallout` |

## Shape Interfaces

### `ShapeProps`

 Extends: `PositionProps`, `ObjectNameProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `align?` | `HAlign` | Horizontal alignment @default 'left' |
| `angleRange?` | `[number,number]` | Radius (only for pptx.shapes.PIE, pptx.shapes.ARC, pptx.shapes.BLOCK_ARC) - In the case of pptx.shapes.BLOCK_ARC you have to setup the arcThicknessRatio - values: [0-359, 0-359] @since v3.4.0 @default [270, 0] |
| `arcThicknessRatio?` | `number` | Radius (only for pptx.shapes.BLOCK_ARC) - You have to setup the angleRange values too - values: 0.0-1.0 @since v3.4.0 @default 0.5 |
| `fill?` | `ShapeFillProps` | Shape fill color properties @example { color:'FF0000' } // hex color (red) @example { color:'0088CC', transparency:50 } // hex color, 50% transparent @example { color:pptx.SchemeColor.accent1 } // Theme color Accent1 |
| `flipH?` | `boolean` | Flip shape horizontally? @default false |
| `flipV?` | `boolean` | Flip shape vertical? @default false |
| `hyperlink?` | `HyperlinkProps` | Add hyperlink to shape @example hyperlink: { url: "https://github.com/gitbrent/pptxgenjs", tooltip: "Visit Homepage" }, |
| `line?` | `ShapeLineProps` | Line options |
| `points?` | `Array<\|{x:Coord,y:Coord,moveTo?:boolean}\|{x:Coord,y:Coord,curve:{type:'arc',hR:Coord,wR:Coord,stAng:number,swAng:number}}\|{x:Coord,y:Coord,curve:{type:'cubic',x1:Coord,y1:Coord,x2:Coord,y2:Coord}}\|{x:Coord,y:Coord,curve:{type:'quadratic',x1:Coord,y1:Coord}}\|{close:true}>` | Points (only for pptx.shapes.CUSTOM_GEOMETRY) - type: 'arc' - `hR` Shape Arc Height Radius - `wR` Shape Arc Width Radius - `stAng` Shape Arc Start Angle - `swAng` Shape Arc Swing Angle @see http://www.datypic.com/sc/ooxml/e-a_arcTo-1.html @example [{ x: 0, y: 0 }, { x: 10, y: 10 }] // draw a line between those two points |
| `rectRadius?` | `number` | Rounded rectangle radius (only for pptx.shapes.ROUNDED_RECTANGLE) - values: 0.0 to 1.0 @default 0 |
| `rotate?` | `number` | Rotation (degrees) - range: -360 to 360 @default 0 @example 180 // rotate 180 degrees |
| `shadow?` | `ShadowProps` | Shadow options TODO: need new demo.js entry for shape shadow |
| `lineSize?` | `number` | @deprecated v3.3.0 |
| `lineDash?` | `'dash'\|'dashDot'\|'lgDash'\|'lgDashDot'\|'lgDashDotDot'\|'solid'\|'sysDash'\|'sysDot'` | @deprecated v3.3.0 |
| `lineHead?` | `'arrow'\|'diamond'\|'none'\|'oval'\|'stealth'\|'triangle'` | @deprecated v3.3.0 |
| `lineTail?` | `'arrow'\|'diamond'\|'none'\|'oval'\|'stealth'\|'triangle'` | @deprecated v3.3.0 |
| `shapeName?` | `string` | Shape name (used instead of default "Shape N" name) @deprecated v3.10.0 - use `objectName` |

### `ShapeFillProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `color?` | `Color` | Fill color - `HexColor` or `ThemeColor` @example 'FF0000' // hex color (red) @example pptx.SchemeColor.text1 // Theme color (Text1) |
| `transparency?` | `number` | Transparency (percent) - MS-PPT > Format Shape > Fill & Line > Fill > Transparency - range: 0-100 @default 0 |
| `type?` | `'none'\|'solid'` | Fill type @default 'solid' |
| `alpha?` | `number` | Transparency (percent) @deprecated v3.3.0 - use `transparency` |

### `ShapeLineProps`

 Extends: `ShapeFillProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `width?` | `number` | Line width (pt) @default 1 |
| `dashType?` | `'solid'\|'dash'\|'dashDot'\|'lgDash'\|'lgDashDot'\|'lgDashDotDot'\|'sysDash'\|'sysDot'` | Dash type @default 'solid' |
| `beginArrowType?` | `'none'\|'arrow'\|'diamond'\|'oval'\|'stealth'\|'triangle'` | Begin arrow type @since v3.3.0 |
| `endArrowType?` | `'none'\|'arrow'\|'diamond'\|'oval'\|'stealth'\|'triangle'` | End arrow type @since v3.3.0 |
| `lineDash?` | `'solid'\|'dash'\|'dashDot'\|'lgDash'\|'lgDashDot'\|'lgDashDotDot'\|'sysDash'\|'sysDot'` | Dash type @deprecated v3.3.0 - use `dashType` |
| `lineHead?` | `'none'\|'arrow'\|'diamond'\|'oval'\|'stealth'\|'triangle'` | @deprecated v3.3.0 - use `beginArrowType` |
| `lineTail?` | `'none'\|'arrow'\|'diamond'\|'oval'\|'stealth'\|'triangle'` | @deprecated v3.3.0 - use `endArrowType` |
| `pt?` | `number` | Line width (pt) @deprecated v3.3.0 - use `width` |
| `size?` | `number` | Line size (pt) @deprecated v3.3.0 - use `width` |

### `ShadowProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `type` | `'outer'\|'inner'\|'none'` | shadow type @default 'none' |
| `opacity?` | `number` | opacity (percent) - range: 0.0-1.0 @example 0.5 // 50% opaque |
| `blur?` | `number` | blur (points) - range: 0-100 @default 0 |
| `angle?` | `number` | angle (degrees) - range: 0-359 @default 0 |
| `offset?` | `number` | shadow offset (points) - range: 0-200 @default 0 |
| `color?` | `HexColor` | shadow color (hex format) @example 'FF3399' |
| `rotateWithShape?` | `boolean` | whether to rotate shadow with shape @default false |

### `HyperlinkProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `slide?` | `number` | Slide number to link to |
| `url?` | `string` | Url to link to |
| `tooltip?` | `string` | Hyperlink Tooltip |
