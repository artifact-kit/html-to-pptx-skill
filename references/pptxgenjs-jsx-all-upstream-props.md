# All Upstream Props

Generated from `pptxgenjs/types/index.d.ts`.

## Type Aliases

### `CHART_NAME`

```ts
type CHART_NAME = 'area'|'bar'|'bar3D'|'bubble'|'doughnut'|'line'|'pie'|'radar'|'scatter'
```

### `SHAPE_NAME`

```ts
type SHAPE_NAME = |'accentBorderCallout1'|'accentBorderCallout2'|'accentBorderCallout3'|'accentCallout1'|'accentCallout2'|'accentCallout3'|'actionButtonBackPrevious'|'actionButtonBeginning'|'actionButtonBlank'|'actionButtonDocument'|'actionButtonEnd'|'actionButtonForwardNext'|'actionButtonHelp'|'actionButtonHome'|'actionButtonInformation'|'actionButtonMovie'|'actionButtonReturn'|'actionButtonSound'|'arc'|'bentArrow'|'bentUpArrow'|'bevel'|'blockArc'|'borderCallout1'|'borderCallout2'|'borderCallout3'|'bracePair'|'bracketPair'|'callout1'|'callout2'|'callout3'|'can'|'chartPlus'|'chartStar'|'chartX'|'chevron'|'chord'|'circularArrow'|'cloud'|'cloudCallout'|'corner'|'cornerTabs'|'cube'|'curvedDownArrow'|'curvedLeftArrow'|'curvedRightArrow'|'curvedUpArrow'|'decagon'|'diagStripe'|'diamond'|'dodecagon'|'donut'|'doubleWave'|'downArrow'|'downArrowCallout'|'ellipse'|'ellipseRibbon'|'ellipseRibbon2'|'flowChartAlternateProcess'|'flowChartCollate'|'flowChartConnector'|'flowChartDecision'|'flowChartDelay'|'flowChartDisplay'|'flowChartDocument'|'flowChartExtract'|'flowChartInputOutput'|'flowChartInternalStorage'|'flowChartMagneticDisk'|'flowChartMagneticDrum'|'flowChartMagneticTape'|'flowChartManualInput'|'flowChartManualOperation'|'flowChartMerge'|'flowChartMultidocument'|'flowChartOfflineStorage'|'flowChartOffpageConnector'|'flowChartOnlineStorage'|'flowChartOr'|'flowChartPredefinedProcess'|'flowChartPreparation'|'flowChartProcess'|'flowChartPunchedCard'|'flowChartPunchedTape'|'flowChartSort'|'flowChartSummingJunction'|'flowChartTerminator'|'folderCorner'|'frame'|'funnel'|'gear6'|'gear9'|'halfFrame'|'heart'|'heptagon'|'hexagon'|'homePlate'|'horizontalScroll'|'irregularSeal1'|'irregularSeal2'|'leftArrow'|'leftArrowCallout'|'leftBrace'|'leftBracket'|'leftCircularArrow'|'leftRightArrow'|'leftRightArrowCallout'|'leftRightCircularArrow'|'leftRightRibbon'|'leftRightUpArrow'|'leftUpArrow'|'lightningBolt'|'line'|'lineInv'|'mathDivide'|'mathEqual'|'mathMinus'|'mathMultiply'|'mathNotEqual'|'mathPlus'|'moon'|'noSmoking'|'nonIsoscelesTrapezoid'|'notchedRightArrow'|'octagon'|'parallelogram'|'pentagon'|'pie'|'pieWedge'|'plaque'|'plaqueTabs'|'plus'|'quadArrow'|'quadArrowCallout'|'rect'|'ribbon'|'ribbon2'|'rightArrow'|'rightArrowCallout'|'rightBrace'|'rightBracket'|'round1Rect'|'round2DiagRect'|'round2SameRect'|'roundRect'|'rtTriangle'|'smileyFace'|'snip1Rect'|'snip2DiagRect'|'snip2SameRect'|'snipRoundRect'|'squareTabs'|'star10'|'star12'|'star16'|'star24'|'star32'|'star4'|'star5'|'star6'|'star7'|'star8'|'stripedRightArrow'|'sun'|'swooshArrow'|'teardrop'|'trapezoid'|'triangle'|'upArrow'|'upArrowCallout'|'upDownArrow'|'upDownArrowCallout'|'uturnArrow'|'verticalScroll'|'wave'|'wedgeEllipseCallout'|'wedgeRectCallout'|'wedgeRoundRectCallout'
```

### `Coord`

```ts
type Coord = number|`${number}%`
```

### `HexColor`

```ts
type HexColor = string
```

### `ThemeColor`

```ts
type ThemeColor = 'tx1'|'tx2'|'bg1'|'bg2'|'accent1'|'accent2'|'accent3'|'accent4'|'accent5'|'accent6'
```

### `Color`

```ts
type Color = HexColor|ThemeColor
```

### `Margin`

```ts
type Margin = number|[number,number,number,number]
```

### `HAlign`

```ts
type HAlign = 'left'|'center'|'right'|'justify'
```

### `VAlign`

```ts
type VAlign = 'top'|'middle'|'bottom'
```

### `MediaType`

```ts
type MediaType = 'audio'|'online'|'video'
```

### `PLACEHOLDER_TYPE`

```ts
type PLACEHOLDER_TYPE = 'title'|'body'|'pic'|'chart'|'tbl'|'media'
```

### `WRITE_OUTPUT_TYPE`

```ts
type WRITE_OUTPUT_TYPE = JSZIP_OUTPUT_TYPE|'STREAM'
```

### `JSZIP_OUTPUT_TYPE`

```ts
type JSZIP_OUTPUT_TYPE = 'arraybuffer'|'base64'|'binarystring'|'blob'|'nodebuffer'|'uint8array'
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

### `PositionProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `x?` | `Coord` | Horizontal position - inches or percentage @example 10.25 // position in inches @example '75%' // position as percentage of slide size |
| `y?` | `Coord` | Vertical position - inches or percentage @example 10.25 // position in inches @example '75%' // position as percentage of slide size |
| `h?` | `Coord` | Height - inches or percentage @example 10.25 // height in inches @example '75%' // height as percentage of slide size |
| `w?` | `Coord` | Width - inches or percentage @example 10.25 // width in inches @example '75%' // width as percentage of slide size |

### `DataOrPathProps`

Either `data` or `path` is required



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `path?` | `string` | URL or relative path @example 'https://onedrives.com/myimg.png` // retrieve image via URL @example '/home/gitbrent/images/myimg.png` // retrieve image via local path |
| `data?` | `string` | base64-encoded string - Useful for avoiding potential path/server issues @example 'image/png;base64,iVtDafDrBF[...]=' // pre-encoded image in base-64 |

### `BackgroundProps`

 Extends: `DataOrPathProps`, `ShapeFillProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `fill?` | `HexColor` | Color (hex format) @deprecated v3.6.0 - use `ShapeFillProps` instead |
| `src?` | `string` | source URL @deprecated v3.6.0 - use `DataOrPathProps` instead - remove in v4.0.0 |

### `BorderProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `type?` | `'none'\|'dash'\|'solid'` | Border type @default solid |
| `color?` | `HexColor` | Border color (hex) @example 'FF3399' @default '666666' |
| `pt?` | `number` | Border size (points) @default 1 |

### `HyperlinkProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `slide?` | `number` | Slide number to link to |
| `url?` | `string` | Url to link to |
| `tooltip?` | `string` | Hyperlink Tooltip |

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

### `TextBaseProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `align?` | `HAlign` | Horizontal alignment @default 'left' |
| `bold?` | `boolean` | Bold style @default false |
| `breakLine?` | `boolean` | Add a line-break @default false |
| `bullet?` | `\|boolean\|{/** * Bullet type * @default bullet */ type?:'bullet'\|'number' /** * Bullet character code(unicode)* @since v3.3.0 * @example '25BA' // 'BLACK RIGHT-POINTING POINTER'(U+25BA)*/ characterCode?:string /** * Indentation(space between bullet and text)(points)* @since v3.3.0 * @default 27 // DEF_BULLET_MARGIN * @example 10 // Indents text 10 points from bullet */ indent?:number /** * Number type * @since v3.3.0 * @example 'romanLcParenR' // roman numerals lower-case with paranthesis right */ numberType?:\|'alphaLcParenBoth'\|'alphaLcParenR'\|'alphaLcPeriod'\|'alphaUcParenBoth'\|'alphaUcParenR'\|'alphaUcPeriod'\|'arabicParenBoth'\|'arabicParenR'\|'arabicPeriod'\|'arabicPlain'\|'romanLcParenBoth'\|'romanLcParenR'\|'romanLcPeriod'\|'romanUcParenBoth'\|'romanUcParenR'\|'romanUcPeriod' /** * Number bullets start at * @since v3.3.0 * @default 1 * @example 10 // numbered bullets start with 10 */ numberStartAt?:number // DEPRECATED /** * Bullet code(unicode)* @deprecated v3.3.0 - use \`characterCode\` */ code?:string /** * Margin between bullet and text * @since v3.2.1 * @deplrecated v3.3.0 - use \`indent\` */ marginPt?:number /** * Number to start with(only applies to type:number)* @deprecated v3.3.0 - use \`numberStartAt\` */ startAt?:number /** * Number type * @deprecated v3.3.0 - use \`numberType\` */ style?:string}` | Add standard or custom bullet - use `true` for standard bullet - pass object options for custom bullet @default false |
| `color?` | `Color` | Text color - `HexColor` or `ThemeColor` - MS-PPT > Format Shape > Text Options > Text Fill & Outline > Text Fill > Color @example 'FF0000' // hex color (red) @example pptx.SchemeColor.text1 // Theme color (Text1) |
| `fontFace?` | `string` | Font face name @example 'Arial' // Arial font |
| `fontSize?` | `number` | Font size @example 12 // Font size 12 |
| `highlight?` | `HexColor` | Text highlight color (hex format) @example 'FFFF00' // yellow |
| `italic?` | `boolean` | italic style @default false |
| `lang?` | `string` | language - ISO 639-1 standard language code @default 'en-US' // english US @example 'fr-CA' // french Canadian |
| `softBreakBefore?` | `boolean` | Add a soft line-break (shift+enter) before line text content @default false @since v3.5.0 |
| `tabStops?` | `Array<{position:number,alignment?:'l'\|'r'\|'ctr'\|'dec'}>` | tab stops - PowerPoint: Paragraph > Tabs > Tab stop position @example [{ position:1 }, { position:3 }] // Set first tab stop to 1 inch, set second tab stop to 3 inches |
| `textDirection?` | `'horz'\|'vert'\|'vert270'\|'wordArtVert'` | text direction `horz` = horizontal `vert` = rotate 90^ `vert270` = rotate 270^ `wordArtVert` = stacked @default 'horz' |
| `transparency?` | `number` | Transparency (percent) - MS-PPT > Format Shape > Text Options > Text Fill & Outline > Text Fill > Transparency - range: 0-100 @default 0 |
| `underline?` | `{style?:\|'dash'\|'dashHeavy'\|'dashLong'\|'dashLongHeavy'\|'dbl'\|'dotDash'\|'dotDashHeave'\|'dotDotDash'\|'dotDotDashHeavy'\|'dotted'\|'dottedHeavy'\|'heavy'\|'none'\|'sng'\|'wavy'\|'wavyDbl'\|'wavyHeavy' color?:Color}` | underline properties - PowerPoint: Font > Color & Underline > Underline Style/Underline Color @default (none) |
| `valign?` | `VAlign` | vertical alignment @default 'top' |

### `ThemeProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `headFontFace?` | `string` | Headings font face name @example 'Arial Narrow' @default 'Calibri Light' |
| `bodyFontFace?` | `string` | Body font face name @example 'Arial' @default 'Calibri' |

### `ImageProps`

 Extends: `PositionProps`, `DataOrPathProps`, `ObjectNameProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `altText?` | `string` | Alt Text value ("How would you describe this object and its contents to someone who is blind?") - PowerPoint: [right-click on an image] > "Edit Alt Text..." |
| `flipH?` | `boolean` | Flip horizontally? @default false |
| `flipV?` | `boolean` | Flip vertical? @default false |
| `hyperlink?` | `HyperlinkProps` | PptxGenJS upstream option. |
| `placeholder?` | `string` | Placeholder type - values: 'body' \| 'header' \| 'footer' \| 'title' \| et. al. @example 'body' @see https://docs.microsoft.com/en-us/office/vba/api/powerpoint.ppplaceholdertype |
| `rotate?` | `number` | Image rotation (degrees) - range: -360 to 360 @default 0 @example 180 // rotate image 180 degrees |
| `rounding?` | `boolean` | Enable image rounding @default false |
| `shadow?` | `ShadowProps` | Shadow Props - MS-PPT > Format Picture > Shadow @example { type: 'outer', color: '000000', opacity: 0.5, blur: 20, offset: 20, angle: 270 } |
| `sizing?` | `{/** * Sizing type */ type:'contain'\|'cover'\|'crop' /** * Image width * - inches or percentage * @example 10.25 // position in inches * @example '75%' // position as percentage of slide size */ w:Coord /** * Image height * - inches or percentage * @example 10.25 // position in inches * @example '75%' // position as percentage of slide size */ h:Coord /** * Offset from left to crop image * - \`crop\` only * - inches or percentage * @example 10.25 // position in inches * @example '75%' // position as percentage of slide size */ x?:Coord /** * Offset from top to crop image * - \`crop\` only * - inches or percentage * @example 10.25 // position in inches * @example '75%' // position as percentage of slide size */ y?:Coord}` | Image sizing options |
| `transparency?` | `number` | Transparency (percent) - MS-PPT > Format Picture > Picture > Picture Transparency > Transparency - range: 0-100 @default 0 @example 25 // 25% transparent |

### `MediaProps`

Add media (audio/video) to slide @requires either `link` or `path`

 Extends: `PositionProps`, `DataOrPathProps`, `ObjectNameProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `type` | `MediaType` | Media type - Use 'online' to embed a YouTube video (only supported in recent versions of PowerPoint) |
| `cover?` | `string` | Cover image @since 3.9.0 @default "play button" image, gray background |
| `extn?` | `string` | media file extension - use when the media file path does not already have an extension, ex: "/folder/SomeSong" @since 3.9.0 @default extension from file provided |
| `link?` | `string` | video embed link - works with YouTube - other sites may not show correctly in PowerPoint @example 'https://www.youtube.com/embed/Dph6ynRVyUc' // embed a youtube video |
| `path?` | `string` | full or local path @example 'https://freesounds/simpsons/bart.mp3' // embed mp3 audio clip from server @example '/sounds/simpsons_haha.mp3' // embed mp3 audio clip from local directory |

### `TableCellProps`

 Extends: `TextBaseProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `autoPageCharWeight?` | `number` | Auto-paging character weight - adjusts how many characters are used before lines wrap - range: -1.0 to 1.0 @see https://gitbrent.github.io/PptxGenJS/docs/api-tables.html @default 0.0 @example 0.5 // lines are longer (increases the number of characters that can fit on a given line) |
| `autoPageLineWeight?` | `number` | Auto-paging line weight - adjusts how many lines are used before slides wrap - range: -1.0 to 1.0 @see https://gitbrent.github.io/PptxGenJS/docs/api-tables.html @default 0.0 @example 0.5 // tables are taller (increases the number of lines that can fit on a given slide) |
| `border?` | `BorderProps\|[BorderProps,BorderProps,BorderProps,BorderProps]` | Cell border |
| `colspan?` | `number` | Cell colspan |
| `fill?` | `ShapeFillProps` | Fill color @example { color:'FF0000' } // hex color (red) @example { color:'0088CC', transparency:50 } // hex color, 50% transparent @example { color:pptx.SchemeColor.accent1 } // theme color Accent1 |
| `hyperlink?` | `HyperlinkProps` | PptxGenJS upstream option. |
| `margin?` | `Margin` | Cell margin (inches) @default 0 |
| `rowspan?` | `number` | Cell rowspan |

### `TableProps`

 Extends: `PositionProps`, `TextBaseProps`, `ObjectNameProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `autoPage?` | `boolean` | Whether to enable auto-paging - auto-paging creates new slides as content overflows a slide @default false |
| `autoPageCharWeight?` | `number` | Auto-paging character weight - adjusts how many characters are used before lines wrap - range: -1.0 to 1.0 @see https://gitbrent.github.io/PptxGenJS/docs/api-tables.html @default 0.0 @example 0.5 // lines are longer (increases the number of characters that can fit on a given line) |
| `autoPageLineWeight?` | `number` | Auto-paging line weight - adjusts how many lines are used before slides wrap - range: -1.0 to 1.0 @see https://gitbrent.github.io/PptxGenJS/docs/api-tables.html @default 0.0 @example 0.5 // tables are taller (increases the number of lines that can fit on a given slide) |
| `autoPageRepeatHeader?` | `boolean` | Whether table header row(s) should be repeated on each new slide creating by autoPage. Use `autoPageHeaderRows` to designate how many rows comprise the table header (1+). @default false @since v3.3.0 |
| `autoPageHeaderRows?` | `number` | Number of rows that comprise table headers - required when `autoPageRepeatHeader` is set to true. @example 2 - repeats the first two table rows on each new slide created @default 1 @since v3.3.0 |
| `autoPageSlideStartY?` | `number` | The `y` location to use on subsequent slides created by autopaging @default (top margin of Slide) |
| `border?` | `BorderProps\|[BorderProps,BorderProps,BorderProps,BorderProps]` | Table border - single value is applied to all 4 sides - array of values in TRBL order for individual sides |
| `colW?` | `number\|number[]` | Width of table columns (inches) - single value is applied to every column equally based upon `w` - array of values in applied to each column in order @default columns of equal width based upon `w` |
| `fill?` | `ShapeFillProps` | Cell background color @example { color:'FF0000' } // hex color (red) @example { color:'0088CC', transparency:50 } // hex color, 50% transparent @example { color:pptx.SchemeColor.accent1 } // theme color Accent1 |
| `margin?` | `Margin` | Cell margin (inches) - affects all table cells, is superceded by cell options |
| `rowH?` | `number\|number[]` | Height of table rows (inches) - single value is applied to every row equally based upon `h` - array of values in applied to each row in order @default rows of equal height based upon `h` |
| `verbose?` | `boolean` | DEV TOOL: Verbose Mode (to console) - tell the library to provide an almost ridiculous amount of detail during auto-paging calculations @default false // obviously |
| `newSlideStartY?` | `number` | @deprecated v3.3.0 - use `autoPageSlideStartY` |

### `TextPropsOptions`

 Extends: `PositionProps`, `DataOrPathProps`, `TextBaseProps`, `ObjectNameProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `baseline?` | `number` | PptxGenJS upstream option. |
| `charSpacing?` | `number` | Character spacing |
| `fit?` | `'none'\|'shrink'\|'resize'` | Text fit options MS-PPT > Format Shape > Shape Options > Text Box > "[unlabeled group]": [3 options below] - 'none' = Do not Autofit - 'shrink' = Shrink text on overflow - 'resize' = Resize shape to fit text **Note** 'shrink' and 'resize' only take effect after editing text/resize shape. Both PowerPoint and Word dynamically calculate a scaling factor and apply it when edit/resize occurs. There is no way for this library to trigger that behavior, sorry. @since v3.3.0 @default "none" |
| `fill?` | `ShapeFillProps` | Shape fill @example { color:'FF0000' } // hex color (red) @example { color:'0088CC', transparency:50 } // hex color, 50% transparent @example { color:pptx.SchemeColor.accent1 } // theme color Accent1 |
| `flipH?` | `boolean` | Flip shape horizontally? @default false |
| `flipV?` | `boolean` | Flip shape vertical? @default false |
| `glow?` | `TextGlowProps` | PptxGenJS upstream option. |
| `hyperlink?` | `HyperlinkProps` | PptxGenJS upstream option. |
| `indentLevel?` | `number` | PptxGenJS upstream option. |
| `isTextBox?` | `boolean` | PptxGenJS upstream option. |
| `line?` | `ShapeLineProps` | PptxGenJS upstream option. |
| `lineSpacing?` | `number` | Line spacing (pt) - PowerPoint: Paragraph > Indents and Spacing > Line Spacing: > "Exactly" @example 28 // 28pt |
| `lineSpacingMultiple?` | `number` | line spacing multiple (percent) - range: 0.0-9.99 - PowerPoint: Paragraph > Indents and Spacing > Line Spacing: > "Multiple" @example 1.5 // 1.5X line spacing @since v3.5.0 |
| `margin?` | `Margin` | Margin (points) - PowerPoint: Format Shape > Shape Options > Size & Properties > Text Box > Left/Right/Top/Bottom margin @default "Normal" margin in PowerPoint [3.5, 7.0, 3.5, 7.0] // (this library sets no value, but PowerPoint defaults to "Normal" [0.05", 0.1", 0.05", 0.1"]) @example 0 // Top/Right/Bottom/Left margin 0 [0.0" in powerpoint] @example 10 // Top/Right/Bottom/Left margin 10 [0.14" in powerpoint] @example [10,5,10,5] // Top margin 10, Right margin 5, Bottom margin 10, Left margin 5 |
| `outline?` | `{color:Color,size:number}` | PptxGenJS upstream option. |
| `paraSpaceAfter?` | `number` | PptxGenJS upstream option. |
| `paraSpaceBefore?` | `number` | PptxGenJS upstream option. |
| `placeholder?` | `string` | PptxGenJS upstream option. |
| `rectRadius?` | `number` | Rounded rectangle radius (only for pptx.shapes.ROUNDED_RECTANGLE) - values: 0.0 to 1.0 @default 0 |
| `rotate?` | `number` | Rotation (degrees) - range: -360 to 360 @default 0 @example 180 // rotate 180 degrees |
| `rtlMode?` | `boolean` | Whether to enable right-to-left mode @default false |
| `shadow?` | `ShadowProps` | PptxGenJS upstream option. |
| `shape?` | `SHAPE_NAME` | PptxGenJS upstream option. |
| `strike?` | `boolean\|'dblStrike'\|'sngStrike'` | PptxGenJS upstream option. |
| `subscript?` | `boolean` | PptxGenJS upstream option. |
| `superscript?` | `boolean` | PptxGenJS upstream option. |
| `valign?` | `VAlign` | Vertical alignment @default middle |
| `vert?` | `'eaVert'\|'horz'\|'mongolianVert'\|'vert'\|'vert270'\|'wordArtVert'\|'wordArtVertRtl'` | PptxGenJS upstream option. |
| `wrap?` | `boolean` | Text wrap @since v3.3.0 @default true |
| `autoFit?` | `boolean` | Whether "Fit to Shape?" is enabled @deprecated v3.3.0 - use `fit` |
| `shrinkText?` | `boolean` | Whather "Shrink Text on Overflow?" is enabled @deprecated v3.3.0 - use `fit` |
| `inset?` | `number` | Inset @deprecated v3.10.0 - use `margin` |
| `lineDash?` | `'solid'\|'dash'\|'dashDot'\|'lgDash'\|'lgDashDot'\|'lgDashDotDot'\|'sysDash'\|'sysDot'` | Dash type @deprecated v3.3.0 - use `line.dashType` |
| `lineHead?` | `'none'\|'arrow'\|'diamond'\|'oval'\|'stealth'\|'triangle'` | @deprecated v3.3.0 - use `line.beginArrowType` |
| `lineSize?` | `number` | @deprecated v3.3.0 - use `line.width` |
| `lineTail?` | `'none'\|'arrow'\|'diamond'\|'oval'\|'stealth'\|'triangle'` | @deprecated v3.3.0 - use `line.endArrowType` |

### `TextProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `text?` | `string` | PptxGenJS upstream option. |
| `options?` | `TextPropsOptions` | PptxGenJS upstream option. |

### `WriteProps`

 Extends: `WriteBaseProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `outputType?` | `WRITE_OUTPUT_TYPE` | Output type - values: 'arraybuffer' \| 'base64' \| 'binarystring' \| 'blob' \| 'nodebuffer' \| 'uint8array' \| 'STREAM' @default 'blob' |

### `WriteFileProps`

 Extends: `WriteBaseProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `fileName?` | `string` | Export file name @default 'Presentation.pptx' |

### `SectionProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `title` | `string` | Section title |
| `order?` | `number` | Section order - uses to add section at any index - values: 1-n |

### `PresLayout`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `name` | `string` | Layout Name @example 'LAYOUT_WIDE' |
| `width` | `number` | PptxGenJS upstream option. |
| `height` | `number` | PptxGenJS upstream option. |

### `SlideNumberProps`

 Extends: `PositionProps`, `TextBaseProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `margin?` | `Margin` | margin (points) |

### `SlideMasterProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `title` | `string` | Unique name for this master |
| `background?` | `BackgroundProps` | PptxGenJS upstream option. |
| `margin?` | `Margin` | PptxGenJS upstream option. |
| `slideNumber?` | `SlideNumberProps` | PptxGenJS upstream option. |
| `objects?` | `Array<\|{chart:IChartOpts}\|{image:ImageProps}\|{line:ShapeProps}\|{rect:ShapeProps}\|{text:TextProps}\|{placeholder:{options:PlaceholderProps /** * Text to be shown in placeholder(shown until user focuses textbox or adds text)* - Leave blank to have powerpoint show default phrase(ex:"Click to add title")*/ text?:string}}>` | PptxGenJS upstream option. |
| `bkgd?` | `string\|BackgroundProps` | @deprecated v3.3.0 - use `background` |

### `AddSlideProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `masterName?` | `string` | PptxGenJS upstream option. |
| `sectionTitle?` | `string` | PptxGenJS upstream option. |

### `PresentationProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `author` | `string` | PptxGenJS upstream option. |
| `company` | `string` | PptxGenJS upstream option. |
| `layout` | `string` | PptxGenJS upstream option. |
| `masterSlide` | `PresSlide` | PptxGenJS upstream option. |
| `presLayout` | `PresLayout` | Presentation's layout read-only |
| `revision` | `string` | PptxGenJS upstream option. |
| `rtlMode` | `boolean` | Whether to enable right-to-left mode @default false |
| `subject` | `string` | PptxGenJS upstream option. |
| `theme` | `ThemeProps` | PptxGenJS upstream option. |
| `title` | `string` | PptxGenJS upstream option. |

### `PlaceholderProps`

 Extends: `PositionProps`, `TextBaseProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `name` | `string` | PptxGenJS upstream option. |
| `type` | `PLACEHOLDER_TYPE` | PptxGenJS upstream option. |
| `margin?` | `Margin` | margin (points) |

### `ObjectNameProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `objectName?` | `string` | Object name - used instead of default "Object N" name - PowerPoint: Home > Arrange > Selection Pane... @since v3.10.0 @default 'Object 1' @example 'Antenna Design 9' |

### `TableToSlidesProps`

 Extends: `TableProps`.

| Prop | Type | Comment |
| :-- | :-- | :-- |
| `addImage?` | `{image:DataOrPathProps,options:PositionProps}` | Add an image to slide(s) created during autopaging - `image` prop requires either `path` or `data` - see `DataOrPathProps` for details on `image` props - see `PositionProps` for details on `options` props |
| `addShape?` | `{shapeName:SHAPE_NAME,options:ShapeProps}` | Add a shape to slide(s) created during autopaging |
| `addTable?` | `{rows:TableRow[],options:TableProps}` | Add a table to slide(s) created during autopaging |
| `addText?` | `{text:TextProps[],options:TextPropsOptions}` | Add a text object to slide(s) created during autopaging |
| `autoPage?` | `boolean` | Whether to enable auto-paging - auto-paging creates new slides as content overflows a slide @default true |
| `autoPageCharWeight?` | `number` | Auto-paging character weight - adjusts how many characters are used before lines wrap - range: -1.0 to 1.0 @see https://gitbrent.github.io/PptxGenJS/docs/api-tables.html @default 0.0 @example 0.5 // lines are longer (increases the number of characters that can fit on a given line) |
| `autoPageLineWeight?` | `number` | Auto-paging line weight - adjusts how many lines are used before slides wrap - range: -1.0 to 1.0 @see https://gitbrent.github.io/PptxGenJS/docs/api-tables.html @default 0.0 @example 0.5 // tables are taller (increases the number of lines that can fit on a given slide) |
| `autoPageRepeatHeader?` | `boolean` | Whether to repeat head row(s) on new tables created by autopaging @since v3.3.0 @default false |
| `autoPageSlideStartY?` | `number` | The `y` location to use on subsequent slides created by autopaging @default (top margin of Slide) |
| `colW?` | `number\|number[]` | Column widths (inches) |
| `masterSlideName?` | `string` | Master slide name - define a master slide to have your auto-paged slides have corporate design, etc. @see https://gitbrent.github.io/PptxGenJS/docs/masters.html |
| `slideMargin?` | `Margin` | Slide margin - this margin will be across all slides created by auto-paging |
| `addHeaderToEach?` | `boolean` | @deprecated v3.3.0 - use `autoPageRepeatHeader` |
| `newSlideStartY?` | `number` | @deprecated v3.3.0 - use `autoPageSlideStartY` |

### `TableCell`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `text?` | `string\|TableCell[]` | PptxGenJS upstream option. |
| `options?` | `TableCellProps` | PptxGenJS upstream option. |

### `TextGlowProps`



| Prop | Type | Comment |
| :-- | :-- | :-- |
| `color?` | `HexColor` | Border color (hex format) @example 'FF3399' |
| `opacity` | `number` | opacity (0.0 - 1.0) @example 0.5 50% opaque |
| `size` | `number` | size (points) |

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
