# Component Selection

## Root Components

| Component | Maps to | Use when | Props interface |
| :-- | :-- | :-- | :-- |
| `Deck` | `new PptxGenJS()` | Root presentation. | `DeckProps` |
| `Presentation` | `Deck alias` | Readable alias for Deck. | `DeckProps` |

## Structure Components

| Component | Maps to | Use when | Props interface |
| :-- | :-- | :-- | :-- |
| `Slide` | `pptx.addSlide` | Create a slide. | `SlideProps` |
| `Layout` | `pptx.defineLayout` | Define an additional custom layout. | `LayoutProps` |
| `Section` | `pptx.addSection` | Group nested slides into a PowerPoint section. | `SectionProps` |
| `Master` | `pptx.defineSlideMaster` | Define a reusable slide master. | `MasterProps` |
| `Placeholder` | `SlideMasterProps.objects[].placeholder` | Add a placeholder inside Master. | `PlaceholderProps` |

## Text Components

| Component | Maps to | Use when | Props interface |
| :-- | :-- | :-- | :-- |
| `Text` | `slide.addText` | Text box, rich text container, or text inside a shape. | `TextProps` |
| `TextRun` | `PptxGenJS.TextProps[] item` | Per-run formatting inside Text. | `TextRunProps` |
| `Notes` | `slide.addNotes` | Speaker notes. | `NotesProps` |

## Shape Components

| Component | Maps to | Use when | Props interface |
| :-- | :-- | :-- | :-- |
| `Rect` | `slide.addShape('rect')` | Plain rectangle. | `RectProps` |
| `RoundRect` | `slide.addShape('roundRect')` | Rounded rectangle; supports rectRadius. | `RoundRectProps` |
| `Ellipse` | `slide.addShape('ellipse')` | Ellipse or oval. | `EllipseProps` |
| `Line` | `slide.addShape('line')` | Line or arrow line. | `LineProps` |
| `LineBetween` | `slide.addShape('line') with normalized x/y/w/h and flipH/flipV` | Line or arrow from endpoint A to endpoint B; best for SVG line/path endpoints and diagonal or vertical arrows. | `LineBetweenProps` |
| `Arc` | `slide.addShape('arc')` | Arc shape; supports angleRange. | `ArcProps` |
| `BlockArc` | `slide.addShape('blockArc')` | Thick arc; supports angleRange and arcThicknessRatio. | `BlockArcProps` |
| `PieShape` | `slide.addShape('pie')` | Pie-slice shape; not a data chart. | `PieShapeProps` |
| `CustomGeometry` | `slide.addShape('custGeom')` | Editable custom path geometry, especially SVG path primitives converted to PowerPoint points. | `CustomGeometryProps` |
| `Triangle` | `slide.addShape('triangle')` | Triangle shape. | `TriangleProps` |
| `RightTriangle` | `slide.addShape('rtTriangle')` | Right triangle. | `TriangleProps` |
| `Diamond` | `slide.addShape('diamond')` | Diamond shape. | `DiamondProps` |
| `Pentagon` | `slide.addShape('pentagon')` | Pentagon shape. | `PentagonProps` |
| `Hexagon` | `slide.addShape('hexagon')` | Hexagon shape. | `HexagonProps` |
| `Star` | `slide.addShape('star5')` | Default five-point star. | `StarProps` |
| `Star4` | `slide.addShape('star4')` | Four-point star. | `StarProps` |
| `Star5` | `slide.addShape('star5')` | Five-point star. | `StarProps` |
| `Star6` | `slide.addShape('star6')` | Six-point star. | `StarProps` |
| `Star8` | `slide.addShape('star8')` | Eight-point star. | `StarProps` |
| `Star10` | `slide.addShape('star10')` | Ten-point star. | `StarProps` |
| `LeftArrow` | `slide.addShape('leftArrow')` | Left arrow block shape. | `ArrowProps` |
| `RightArrow` | `slide.addShape('rightArrow')` | Right arrow block shape. | `ArrowProps` |
| `UpArrow` | `slide.addShape('upArrow')` | Up arrow block shape. | `ArrowProps` |
| `DownArrow` | `slide.addShape('downArrow')` | Down arrow block shape. | `ArrowProps` |
| `LeftRightArrow` | `slide.addShape('leftRightArrow')` | Bidirectional left/right arrow. | `ArrowProps` |
| `UpDownArrow` | `slide.addShape('upDownArrow')` | Bidirectional up/down arrow. | `ArrowProps` |
| `Chevron` | `slide.addShape('chevron')` | Chevron shape. | `ShapeOptionsProps` |
| `Cloud` | `slide.addShape('cloud')` | Cloud shape. | `ShapeOptionsProps` |
| `Heart` | `slide.addShape('heart')` | Heart shape. | `ShapeOptionsProps` |
| `Donut` | `slide.addShape('donut')` | Donut shape. | `ShapeOptionsProps` |
| `Plus` | `slide.addShape('plus')` | Plus/cross shape. | `ShapeOptionsProps` |

## Escape Hatch Components

| Component | Maps to | Use when | Props interface |
| :-- | :-- | :-- | :-- |
| `Shape` | `slide.addShape(shape, options)` | Any PptxGenJS shape not exposed as a dedicated component. | `ShapeProps` |
| `Chart` | `slide.addChart(type, data, options)` | Multi-chart or any raw chart type usage. | `ChartProps` |
| `Raw` | `custom render callback` | Newest or unsupported PptxGenJS APIs. | `RawProps` |

## Chart Components

| Component | Maps to | Use when | Props interface |
| :-- | :-- | :-- | :-- |
| `AreaChart` | `slide.addChart('area')` | Area chart. | `AreaChartProps` |
| `BarChart` | `slide.addChart('bar')` | Bar or column chart. | `BarChartProps` |
| `Bar3DChart` | `slide.addChart('bar3D')` | 3D bar chart. | `Bar3DChartProps` |
| `BubbleChart` | `slide.addChart('bubble')` | Bubble chart; data can include sizes. | `BubbleChartProps` |
| `DoughnutChart` | `slide.addChart('doughnut')` | Doughnut chart. | `DoughnutChartProps` |
| `LineChart` | `slide.addChart('line')` | Line chart. | `LineChartProps` |
| `PieChart` | `slide.addChart('pie')` | Pie data chart. | `PieChartProps` |
| `RadarChart` | `slide.addChart('radar')` | Radar chart. | `RadarChartProps` |
| `ScatterChart` | `slide.addChart('scatter')` | Scatter chart. | `ScatterChartProps` |

## Media Components

| Component | Maps to | Use when | Props interface |
| :-- | :-- | :-- | :-- |
| `Image` | `slide.addImage` | Image by path or data URI/base64. | `ImageProps` |
| `Media` | `slide.addMedia` | Audio, video, or online media. | `MediaProps` |

## Table Components

| Component | Maps to | Use when | Props interface |
| :-- | :-- | :-- | :-- |
| `Table` | `slide.addTable` | PowerPoint table. | `TableProps` |
| `TableRow` | `PptxGenJS.TableRow` | Declarative row inside Table. | `TableRowProps` |
| `TableCell` | `PptxGenJS.TableCell` | Declarative cell inside TableRow. | `TableCellProps` |
| `TableToSlides` | `pptx.tableToSlides` | Convert an HTML table in browser/runtime DOM. | `TableToSlidesProps` |
