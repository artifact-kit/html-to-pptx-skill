# Chart Props

Generated from `pptxgenjs/types/index.d.ts`.

## Type Aliases

### `CHART_NAME`

```ts
type CHART_NAME = 'area'|'bar'|'bar3D'|'bubble'|'doughnut'|'line'|'pie'|'radar'|'scatter'
```

### `ChartAxisTickMark`

```ts
type ChartAxisTickMark = 'none'|'inside'|'outside'|'cross'
```

### `ChartLineCap`

```ts
type ChartLineCap = 'flat'|'round'|'square'
```

## Interfaces

### `OptsChartData`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `labels?` | `string[]\|string[][]` | category labels @example ['Year 2000', 'Year 2010', 'Year 2020'] // single-level category axes labels @example [['Year 2000', 'Year 2010', 'Year 2020'], ['Decades', '', '']] // multi-level category axes labels @since `labels` string[][] type added v3.11.0 |
| `name?` | `string` | series name @example 'Locations' |
| `sizes?` | `number[]` | bubble sizes @example [5, 1, 5, 1] |
| `values?` | `number[]` | category values @example [2000, 2010, 2020] |

### `OptsChartGridLine`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `cap?` | `ChartLineCap` | MS-PPT > Chart format > Format Major Gridlines > Line > Cap type - line cap type @default flat |
| `color?` | `HexColor` | Gridline color (hex) @example 'FF3399' |
| `size?` | `number` | Gridline size (points) |
| `style?` | `'solid'\|'dash'\|'dot'\|'none'` | Gridline style |

### `IChartMulti`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `type` | `CHART_NAME` | PptxGenJS upstream option. |
| `data` | `OptsChartData[]` | PptxGenJS upstream option. |
| `options` | `IChartOpts` | PptxGenJS upstream option. |

### `IChartPropsFillLine`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `border?` | `BorderProps` | PowerPoint: Format Chart Area/Plot > Border ["Line"] @example border: {color: 'FF0000', pt: 1} // hex RGB color, 1 pt line |
| `fill?` | `ShapeFillProps` | PowerPoint: Format Chart Area/Plot Area > Fill @example fill: {color: '696969'} // hex RGB color value @example fill: {color: pptx.SchemeColor.background2} // Theme color value @example fill: {transparency: 50} // 50% transparency |

### `IChartAreaProps`

 Extends: `IChartPropsFillLine`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `roundedCorners?` | `boolean` | Whether the chart area has rounded corners - only applies when either `fill` or `border` is used @default true @since v3.11 |

### `IChartPropsBase`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `axisPos?` | `'b'\|'l'\|'r'\|'t'` | Axis position |
| `chartColors?` | `HexColor[]` | PptxGenJS upstream option. |
| `chartColorsOpacity?` | `number` | opacity (0 - 100) @example 50 // 50% opaque |
| `dataBorder?` | `BorderProps` | PptxGenJS upstream option. |
| `displayBlanksAs?` | `string` | PptxGenJS upstream option. |
| `invertedColors?` | `HexColor[]` | PptxGenJS upstream option. |
| `lang?` | `string` | PptxGenJS upstream option. |
| `layout?` | `PositionProps` | PptxGenJS upstream option. |
| `shadow?` | `ShadowProps` | PptxGenJS upstream option. |
| `showLabel?` | `boolean` | @default false |
| `showLeaderLines?` | `boolean` | PptxGenJS upstream option. |
| `showLegend?` | `boolean` | @default false |
| `showPercent?` | `boolean` | @default false |
| `showSerName?` | `boolean` | @default false |
| `showTitle?` | `boolean` | @default false |
| `showValue?` | `boolean` | @default false |
| `v3DPerspective?` | `number` | 3D Perspecitve - range: 0-120 @default 30 |
| `v3DRAngAx?` | `boolean` | Right Angle Axes - Shows chart from first-person perspective - Overrides `v3DPerspective` when true - PowerPoint: Chart Options > 3-D Rotation @default false |
| `v3DRotX?` | `number` | X Rotation - PowerPoint: Chart Options > 3-D Rotation - range: 0-359.9 @default 30 |
| `v3DRotY?` | `number` | Y Rotation - range: 0-359.9 @default 30 |
| `chartArea?` | `IChartAreaProps` | PowerPoint: Format Chart Area (Fill & Border/Line) @since v3.11 |
| `plotArea?` | `IChartPropsFillLine` | PowerPoint: Format Plot Area (Fill & Border/Line) @since v3.11 |
| `border?` | `BorderProps` | @deprecated v3.11.0 - use `plotArea.border` |
| `fill?` | `HexColor` | @deprecated v3.11.0 - use `plotArea.fill` |

### `IChartPropsAxisCat`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `catAxes?` | `IChartPropsAxisCat[]` | Multi-Chart prop: array of cat axes |
| `catAxisBaseTimeUnit?` | `string` | PptxGenJS upstream option. |
| `catAxisCrossesAt?` | `number\|'autoZero'` | PptxGenJS upstream option. |
| `catAxisHidden?` | `boolean` | PptxGenJS upstream option. |
| `catAxisLabelColor?` | `string` | PptxGenJS upstream option. |
| `catAxisLabelFontBold?` | `boolean` | PptxGenJS upstream option. |
| `catAxisLabelFontFace?` | `string` | PptxGenJS upstream option. |
| `catAxisLabelFontItalic?` | `boolean` | PptxGenJS upstream option. |
| `catAxisLabelFontSize?` | `number` | PptxGenJS upstream option. |
| `catAxisLabelFrequency?` | `string` | PptxGenJS upstream option. |
| `catAxisLabelPos?` | `'none'\|'low'\|'high'\|'nextTo'` | PptxGenJS upstream option. |
| `catAxisLabelRotate?` | `number` | PptxGenJS upstream option. |
| `catAxisLineColor?` | `string` | PptxGenJS upstream option. |
| `catAxisLineShow?` | `boolean` | PptxGenJS upstream option. |
| `catAxisLineSize?` | `number` | PptxGenJS upstream option. |
| `catAxisLineStyle?` | `'solid'\|'dash'\|'dot'` | PptxGenJS upstream option. |
| `catAxisMajorTickMark?` | `ChartAxisTickMark` | PptxGenJS upstream option. |
| `catAxisMajorTimeUnit?` | `string` | PptxGenJS upstream option. |
| `catAxisMajorUnit?` | `number` | PptxGenJS upstream option. |
| `catAxisMaxVal?` | `number` | PptxGenJS upstream option. |
| `catAxisMinorTickMark?` | `ChartAxisTickMark` | PptxGenJS upstream option. |
| `catAxisMinorTimeUnit?` | `string` | PptxGenJS upstream option. |
| `catAxisMinorUnit?` | `number` | PptxGenJS upstream option. |
| `catAxisMinVal?` | `number` | PptxGenJS upstream option. |
| `catAxisMultiLevelLabels?` | `boolean` | @since v3.11.0 |
| `catAxisOrientation?` | `'minMax'` | PptxGenJS upstream option. |
| `catAxisTitle?` | `string` | PptxGenJS upstream option. |
| `catAxisTitleColor?` | `string` | PptxGenJS upstream option. |
| `catAxisTitleFontFace?` | `string` | PptxGenJS upstream option. |
| `catAxisTitleFontSize?` | `number` | PptxGenJS upstream option. |
| `catAxisTitleRotate?` | `number` | PptxGenJS upstream option. |
| `catGridLine?` | `OptsChartGridLine` | PptxGenJS upstream option. |
| `catLabelFormatCode?` | `string` | PptxGenJS upstream option. |
| `secondaryCatAxis?` | `boolean` | Whether data should use secondary category axis (instead of primary) @default false |
| `showCatAxisTitle?` | `boolean` | PptxGenJS upstream option. |

### `IChartPropsAxisSer`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `serAxisBaseTimeUnit?` | `string` | PptxGenJS upstream option. |
| `serAxisHidden?` | `boolean` | PptxGenJS upstream option. |
| `serAxisLabelColor?` | `string` | PptxGenJS upstream option. |
| `serAxisLabelFontBold?` | `boolean` | PptxGenJS upstream option. |
| `serAxisLabelFontFace?` | `string` | PptxGenJS upstream option. |
| `serAxisLabelFontItalic?` | `boolean` | PptxGenJS upstream option. |
| `serAxisLabelFontSize?` | `number` | PptxGenJS upstream option. |
| `serAxisLabelFrequency?` | `string` | PptxGenJS upstream option. |
| `serAxisLabelPos?` | `'none'\|'low'\|'high'\|'nextTo'` | PptxGenJS upstream option. |
| `serAxisLineColor?` | `string` | PptxGenJS upstream option. |
| `serAxisLineShow?` | `boolean` | PptxGenJS upstream option. |
| `serAxisMajorTimeUnit?` | `string` | PptxGenJS upstream option. |
| `serAxisMajorUnit?` | `number` | PptxGenJS upstream option. |
| `serAxisMinorTimeUnit?` | `string` | PptxGenJS upstream option. |
| `serAxisMinorUnit?` | `number` | PptxGenJS upstream option. |
| `serAxisOrientation?` | `string` | PptxGenJS upstream option. |
| `serAxisTitle?` | `string` | PptxGenJS upstream option. |
| `serAxisTitleColor?` | `string` | PptxGenJS upstream option. |
| `serAxisTitleFontFace?` | `string` | PptxGenJS upstream option. |
| `serAxisTitleFontSize?` | `number` | PptxGenJS upstream option. |
| `serAxisTitleRotate?` | `number` | PptxGenJS upstream option. |
| `serGridLine?` | `OptsChartGridLine` | PptxGenJS upstream option. |
| `serLabelFormatCode?` | `string` | PptxGenJS upstream option. |
| `showSerAxisTitle?` | `boolean` | PptxGenJS upstream option. |

### `IChartPropsAxisVal`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `secondaryValAxis?` | `boolean` | Whether data should use secondary value axis (instead of primary) @default false |
| `showValAxisTitle?` | `boolean` | PptxGenJS upstream option. |
| `valAxes?` | `IChartPropsAxisVal[]` | Multi-Chart prop: array of val axes |
| `valAxisCrossesAt?` | `number\|'autoZero'` | PptxGenJS upstream option. |
| `valAxisDisplayUnit?` | `'billions'\|'hundredMillions'\|'hundreds'\|'hundredThousands'\|'millions'\|'tenMillions'\|'tenThousands'\|'thousands'\|'trillions'` | PptxGenJS upstream option. |
| `valAxisDisplayUnitLabel?` | `boolean` | PptxGenJS upstream option. |
| `valAxisHidden?` | `boolean` | PptxGenJS upstream option. |
| `valAxisLabelColor?` | `string` | PptxGenJS upstream option. |
| `valAxisLabelFontBold?` | `boolean` | PptxGenJS upstream option. |
| `valAxisLabelFontFace?` | `string` | PptxGenJS upstream option. |
| `valAxisLabelFontItalic?` | `boolean` | PptxGenJS upstream option. |
| `valAxisLabelFontSize?` | `number` | PptxGenJS upstream option. |
| `valAxisLabelFormatCode?` | `string` | PptxGenJS upstream option. |
| `valAxisLabelPos?` | `'none'\|'low'\|'high'\|'nextTo'` | PptxGenJS upstream option. |
| `valAxisLabelRotate?` | `number` | PptxGenJS upstream option. |
| `valAxisLineColor?` | `string` | PptxGenJS upstream option. |
| `valAxisLineShow?` | `boolean` | PptxGenJS upstream option. |
| `valAxisLineSize?` | `number` | PptxGenJS upstream option. |
| `valAxisLineStyle?` | `'solid'\|'dash'\|'dot'` | PptxGenJS upstream option. |
| `valAxisLogScaleBase?` | `number` | PowerPoint: Format Axis > Axis Options > Logarithmic scale - Base - range: 2-99 @since v3.5.0 |
| `valAxisMajorTickMark?` | `ChartAxisTickMark` | PptxGenJS upstream option. |
| `valAxisMajorUnit?` | `number` | PptxGenJS upstream option. |
| `valAxisMaxVal?` | `number` | PptxGenJS upstream option. |
| `valAxisMinorTickMark?` | `ChartAxisTickMark` | PptxGenJS upstream option. |
| `valAxisMinVal?` | `number` | PptxGenJS upstream option. |
| `valAxisOrientation?` | `'minMax'` | PptxGenJS upstream option. |
| `valAxisTitle?` | `string` | PptxGenJS upstream option. |
| `valAxisTitleColor?` | `string` | PptxGenJS upstream option. |
| `valAxisTitleFontFace?` | `string` | PptxGenJS upstream option. |
| `valAxisTitleFontSize?` | `number` | PptxGenJS upstream option. |
| `valAxisTitleRotate?` | `number` | PptxGenJS upstream option. |
| `valGridLine?` | `OptsChartGridLine` | PptxGenJS upstream option. |
| `valLabelFormatCode?` | `string` | Value label format code - this also directs Data Table formatting @since v3.3.0 @example '#%' // round percent @example '0.00%' // shows values as '0.00%' @example '$0.00' // shows values as '$0.00' |

### `IChartPropsChartBar`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `bar3DShape?` | `string` | PptxGenJS upstream option. |
| `barDir?` | `string` | PptxGenJS upstream option. |
| `barGapDepthPct?` | `number` | PptxGenJS upstream option. |
| `barGapWidthPct?` | `number` | MS-PPT > Format chart > Format Data Point > Series Options > "Gap Width" - width (percent) - range: `0`-`500` @default 150 |
| `barGrouping?` | `string` | PptxGenJS upstream option. |
| `barOverlapPct?` | `number` | MS-PPT > Format chart > Format Data Point > Series Options > "Series Overlap" - overlap (percent) - range: `-100`-`100` @since v3.9.0 @default 0 |

### `IChartPropsChartDoughnut`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `dataNoEffects?` | `boolean` | PptxGenJS upstream option. |
| `holeSize?` | `number` | PptxGenJS upstream option. |

### `IChartPropsChartLine`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `lineCap?` | `ChartLineCap` | MS-PPT > Chart format > Format Data Series > Line > Cap type - line cap type @default flat |
| `lineDash?` | `'dash'\|'dashDot'\|'lgDash'\|'lgDashDot'\|'lgDashDotDot'\|'solid'\|'sysDash'\|'sysDot'` | MS-PPT > Chart format > Format Data Series > Marker Options > Built-in > Type - line dash type @default solid |
| `lineDataSymbol?` | `'circle'\|'dash'\|'diamond'\|'dot'\|'none'\|'square'\|'triangle'` | MS-PPT > Chart format > Format Data Series > Marker Options > Built-in > Type - marker type @default circle |
| `lineDataSymbolLineColor?` | `string` | MS-PPT > Chart format > Format Data Series > [Marker Options] > Border > Color - border color @default circle |
| `lineDataSymbolLineSize?` | `number` | MS-PPT > Chart format > Format Data Series > [Marker Options] > Border > Width - border width (points) @default 0.75 |
| `lineDataSymbolSize?` | `number` | MS-PPT > Chart format > Format Data Series > Marker Options > Built-in > Size - marker size - range: 2-72 @default 6 |
| `lineSize?` | `number` | MS-PPT > Chart format > Format Data Series > Line > Width - line width (points) - range: 0-1584 @default 2 |
| `lineSmooth?` | `boolean` | MS-PPT > Chart format > Format Data Series > Line > Smoothed line - "Smoothed line" @default false |

### `IChartPropsChartPie`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `dataNoEffects?` | `boolean` | PptxGenJS upstream option. |
| `firstSliceAng?` | `number` | MS-PPT > Format chart > Format Data Series > Series Options > "Angle of first slice" - angle (degrees) - range: 0-359 @since v3.4.0 @default 0 |

### `IChartPropsChartRadar`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `radarStyle?` | `'standard'\|'marker'\|'filled'` | MS-PPT > Chart Type > Waterfall - radar chart type @default standard |

### `IChartPropsDataLabel`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `dataLabelBkgrdColors?` | `boolean` | PptxGenJS upstream option. |
| `dataLabelColor?` | `string` | PptxGenJS upstream option. |
| `dataLabelFontBold?` | `boolean` | PptxGenJS upstream option. |
| `dataLabelFontFace?` | `string` | PptxGenJS upstream option. |
| `dataLabelFontItalic?` | `boolean` | PptxGenJS upstream option. |
| `dataLabelFontSize?` | `number` | PptxGenJS upstream option. |
| `dataLabelFormatCode?` | `string` | Data label format code @example '#%' // round percent @example '0.00%' // shows values as '0.00%' @example '$0.00' // shows values as '$0.00' |
| `dataLabelFormatScatter?` | `'custom'\|'customXY'\|'XY'` | PptxGenJS upstream option. |
| `dataLabelPosition?` | `'b'\|'bestFit'\|'ctr'\|'l'\|'r'\|'t'\|'inEnd'\|'outEnd'` | PptxGenJS upstream option. |

### `IChartPropsDataTable`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `dataTableFontSize?` | `number` | PptxGenJS upstream option. |
| `dataTableFormatCode?` | `string` | Data table format code @since v3.3.0 @example '#%' // round percent @example '0.00%' // shows values as '0.00%' @example '$0.00' // shows values as '$0.00' |
| `showDataTable?` | `boolean` | Whether to show a data table adjacent to the chart @default false |
| `showDataTableHorzBorder?` | `boolean` | PptxGenJS upstream option. |
| `showDataTableKeys?` | `boolean` | PptxGenJS upstream option. |
| `showDataTableOutline?` | `boolean` | PptxGenJS upstream option. |
| `showDataTableVertBorder?` | `boolean` | PptxGenJS upstream option. |

### `IChartPropsLegend`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `legendColor?` | `string` | PptxGenJS upstream option. |
| `legendFontFace?` | `string` | PptxGenJS upstream option. |
| `legendFontSize?` | `number` | PptxGenJS upstream option. |
| `legendPos?` | `'b'\|'l'\|'r'\|'t'\|'tr'` | PptxGenJS upstream option. |

### `IChartPropsTitle`

 Extends: `TextBaseProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `title?` | `string` | PptxGenJS upstream option. |
| `titleAlign?` | `string` | PptxGenJS upstream option. |
| `titleBold?` | `boolean` | PptxGenJS upstream option. |
| `titleColor?` | `string` | PptxGenJS upstream option. |
| `titleFontFace?` | `string` | PptxGenJS upstream option. |
| `titleFontSize?` | `number` | PptxGenJS upstream option. |
| `titlePos?` | `{x:number,y:number}` | PptxGenJS upstream option. |
| `titleRotate?` | `number` | PptxGenJS upstream option. |

### `IChartOpts`

 Extends: `IChartPropsAxisCat`, `IChartPropsAxisSer`, `IChartPropsAxisVal`, `IChartPropsBase`, `IChartPropsChartBar`, `IChartPropsChartDoughnut`, `IChartPropsChartLine`, `IChartPropsChartPie`, `IChartPropsChartRadar`, `IChartPropsDataLabel`, `IChartPropsDataTable`, `IChartPropsLegend`, `IChartPropsTitle`, `ObjectNameProps`, `OptsChartGridLine`, `PositionProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `altText?` | `string` | Alt Text value ("How would you describe this object and its contents to someone who is blind?") - PowerPoint: [right-click on a chart] > "Edit Alt Text..." |
