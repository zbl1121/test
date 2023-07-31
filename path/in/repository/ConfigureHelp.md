# 配置季华绘图编辑器的方式如下：

在Confluence Server/Data Center/Cloud，Jira Server，Quip，嵌入模式，在线和桌面版的季华绘图中，可以进行以下方面的配置：

- 字体和Web字体
- 色彩调色板和主题
- 图形和连接器样式
- 左侧面板中显示的内置库
- 左侧面板中显示的自定义库
- 编辑器外观的CSS
- 左侧面板条目的宽度和高度
- 空白图表和库的XML
- 全局变量
- XML压缩
- 新连接器（边缘）的默认长度
- 自动保存的默认延迟
- 使用外部资源（仅适用于Quip）

在下面的视频中，您将了解到在季华绘图中可以进行哪些自定义配置。

## 配置

**Confluence Data Center或Server：** 以管理员身份进入您的实例设置，向下滚动到左侧导航中的*季华绘图插件*部分，并点击*Configuration*选项卡。

![季华绘图 Configuration in Confluence Server](https://www.drawio.com/assets/img/blog/drawio-configuration-confluence-server.png)

**Confluence Cloud：** 以管理员身份进入您的实例的*Settings*，找到*季华绘图Configuration*部分。

![季华绘图 Configuration in Confluence Cloud](https://www.drawio.com/assets/img/blog/drawio-configuration-confluence-cloud.png)

**Jira Server：** 以管理员身份单击*Settings*图标，选择*Manage apps*（在旧版本的Jira中为*Manage add-ons*）。在左侧导航中打开*季华绘图插件*配置，然后点击*Configuration*选项卡。

![季华绘图 Configuration in Jira Server](https://www.drawio.com/assets/img/blog/jira-server-drawio-configuration.png)

**Quip：** 作为站点管理员，创建一个新的图表，然后选择*Diagrams > Preferences > Advanced*。

![季华绘图 Configuration in Quip](https://www.drawio.com/assets/img/blog/drawio-configuration-quip.gif)

**嵌入模式：** 添加URL参数和JSON代码进行配置。`configure=1`

**在线和桌面版：** 选择*Extras > Configuration*以自定义季华绘图编辑器。

![Access the 季华绘图 configuration via Extras > Configuration](https://www.drawio.com/assets/img/blog/extras-configuration-menu.png)

## 格式

配置以JSON（JavaScript对象表示法）字符串的形式表示，具有以下选项：

- `defaultFonts`：字体家族名称（String）或自定义字体{“fontFamily”：name，“fontUrl”：url}的数组，用于格式面板中的字体下拉列表。示例请参见下文。
- `customFonts`：字体家族名称或自定义字体{“fontFamily”：name，“fontUrl”：url}的数组，在之前添加（9.2.4及更高版本）。例如：[“Helvetica”，{“fontFamily”：“Rock Salt”，“fontUrl”：“https://fonts.googleapis.com/css?family=Rock+Salt”}]。 **注意：** 没有fontUrl的字体必须在服务器上和所有客户端设备上安装，或者使用该选项进行添加（6.5.4及更高版本）。`defaultFonts``fontCss`

![Customise the fonts in 季华绘图](https://www.drawio.com/assets/img/blog/custom-fonts-list-confluence-cloud.png)

- `presetColors`：颜色对话框中上方调色板的颜色代码（颜色代码前没有#号，空白项除外）。`null`
- `customPresetColors`：在之前添加的颜色代码（颜色代码前没有#号，空白项除外）（9.2.5及更高版本）。 `presetColors``#``null`

![The default present colours can be customised in 季华绘图](https://www.drawio.com/assets/img/blog/preset-colours-new-defaults.png)

- defaultColors`：颜色对话框中下方调色板的颜色代码（颜色代码前没有#号，空白项除外）。

![Modify the colour palettes easily with 季华绘图 for Confluence Cloud](https://www.drawio.com/assets/img/blog/large-palette-custom.png)

- `colorNames`：颜色名称，例如{‘FFFFFF’：‘White’，‘000000’：‘Black’}，用作工具提示（大写字母，颜色代码前没有#号）。`#`
- `defaultColorSchemes`：在格式面板顶部的样式部分中可用的颜色方案（使用颜色代码前导符号）。可能的颜色键是，，和（连接器不考虑）。可以添加一个可选的用作工具提示。可以添加一个可选的边框来定义边框宽度和类型的CSS，例如“2px solid”或“3px dashed”（仅设置边框宽度无效，必须包括边框类型）。`#``fill``stroke``gradient``font``font``title`
- `customColorSchemes`：在之前添加的颜色方案

![The default colour schemes in 季华绘图 modify the style colour palette](https://www.drawio.com/assets/img/blog/style-colour-palette.png)

`defaultVertexStyle`或`defaultEdgeStyle`：定义顶点和边（连接器）的初始默认样式。请注意，这里定义的样式会被复制到每个单元格的新单元格的样式中。这意味着这些值会覆盖从其他样式或主题继承的所有内容（这可能在以后的时间得到支持）。因此，建议对默认样式使用最小的一组值。要找到要使用的键/值对，请在应用程序中设置样式，并通过“Edit Style”（编辑样式）（6.5.2及更高版本）找到键和值。

例如，要为所有边和顶点分配Courier New的默认fontFamily（并覆盖所有其他默认样式），可以使用{"defaultVertexStyle": {"fontFamily": "Courier New"}, "defaultEdgeStyle": {"fontFamily": "Courier New"}}。

`styles`：定义了一个对象数组，其中包含*Style*选项卡的颜色（填充、描边和渐变）的定义，如果选择为空。这些对象可以具有应用于顶点和边的填充颜色（`fill`），应用于描边的颜色（`stroke`）和应用于渐变的颜色（`gradient`）。还可以使用`fontColor`来定义文本的颜色，以及`fontFamily`来定义字体样式。空对象将应用默认颜色。

例如：

```
[ {},
{
  "commonStyle": {
    "fontColor": "#5C5C5C",
    "strokeColor": "#006658",
    "fillColor": "#21C0A5"
  }
},
{
  "commonStyle": {
    "fontColor": "#095C86",
    "strokeColor": "#AF45ED",
    "fillColor": "#F694C1"
  },
  "edgeStyle": {
    "strokeColor": "#60E696"
  }
},
{
  "commonStyle": {
    "fontColor": "#E4FDE1",
    "strokeColor": "#028090",
    "fillColor": "#F45B69"
  },
  "graph": {
    "background": "#114B5F",
    "gridColor": "#0B3240"
  }
}
]
```

- `defaultLibraries`: 定义一个以分号分隔的字符串列表，用于在左侧面板中初始显示的库名称（例如）。可能的键包括来自libraries字段的自定义条目ID，或者libs URL参数的键（6.5.2及更高版本）。默认值为。`"general;uml;company-graphics"` `"general;uml;er;bpmn;flowchart;basic;arrows2"`

- `enabledLibraries`: 定义一个字符串数组，其中包含将在“更多形状”对话框中可用的库键。如果将其定义为null，则所有库都将可见。如果将数组留空，则不会显示任何库（例如）（9.2.5及更高版本）。`["general", "uml"]`

- libraries: 定义一个包含附加库和部分的对象数组，用于左侧面板和“更多形状”对话框，格式如下：[section1,...,sectionN]。其中：

  - 每个section的形式为 {title: resource, entries: [entry1,...,entryN]}。
  - 每个entry的形式为 {id: string, preview: string, title: resource, desc: resource, libs: [lib1,..,libN]}。
  - 每个lib的形式为 {title: resource, url: string OR data: string, tags: string}。
  - sections用于“更多形状”对话框中的部分。
  - entries是各部分的条目，每个条目可以关联一个或多个库。每个条目的id必须唯一，preview是作为预览使用的图像的URL，desc是在预览之前或替代预览的描述（支持换行符的预格式化文本）。
  - 在libs中，resource是一个语言资源，定义为{main: string, xy: string}，其中xy可以是任何国家代码（例如es、fr、de），main是如果当前国家代码没有定义字符串，则作为回退（即默认资源）。
  - 此外，在libs中，tags是一个可选的字符串，其中包含以空格分隔的可搜索标签列表。
  - libs可以通过url字段中的URL使用外部资源，也可以直接通过data定义库条目，其中data在库文件中的<mxlibrary>...</mxlibrary>之间包含数组。默认情况下，所有带有data的条目和前20个带有url的条目都将被预取并添加到搜索索引中。要预取其他带有url的条目，请在相应的lib中添加"prefetch": true（9.2.5及更高版本）。

  例如：

```
[ {
 "title": {
 "main": "Company"
 },
 "entries": [ {
"id": "company-graphics",
"title": {
  "main": "Graphics",
  "de": "Grafiken"
},
"desc": {
  "main": "Collection of Graphics for Company",
  "de": "Sammlung von Grafiken für Firma"
},
"libs": [ {
 "title": {
   "main": "Graphics for Company",
   "de": "Grafiken für Firma"
 },
 "data": [ {
     "xml": "jZLBbsMgDIafhmuUgKr1mqZbL5u0VyCJF5BMHIHbpG9fEti6Tqq0A5L5/NuYH4Rq3HLyejIf1AMK9SpU44k4RW5pAFHI0vZCHYWUZVxCvj3JVlu2nLSHkf9TIFPBReMZEkkg8BUz6HUwsMpLoQ50ZrQjNDSO0HGGhl0c/FjFUKMdxhh38XzwEaBuAT8pWLb0kLiAZ9tpfP8jaImZ3C9BnVsyTZEGo6d1MLcMq2nFDC3SQKHovZ4tySj5sogNIfltflXVu0Ot8j1jT1ieerWhbNQJyAH7a5TMtmeTFDtZZIcM2MHkupey2CeqQyLDT/Xd/Bhk/7+393fecg/f4AY=",
     "w": 52.2,
     "h": 70.8,
     "aspect": "fixed"
   } ]
  } ]
 } ]
} ]
```

这个配置与enabledLibraries: []结合使用会产生以下的“更多形状”对话框：
![The More Shape dialog in 季华绘图 after configuring it with a custom library and library category](https://www.drawio.com/assets/img/blog/configured-library.png)

- defaultCustomLibraries: 定义一个加载自定义库的ID数组。 

  - 在Atlassian Confluence中，将ID定义为A1...An，例如{"defaultCustomLibraries": ["A1"]}。要获取自定义库的ID，请将鼠标移动到“选择库”对话框中的条目上或左侧面板中的库标题上，并等待工具提示出现，例如my library (A1)，其中A1是ID。如果没有出现工具提示，请打开图表中的库，保存图表，然后参考附加到使用该图表名称的页面的图表文件中的<mxAtlasLibraries>部分（6.5.2及更高版本）。

  -  或者，您可以使用UencodedURI作为ID从URL加载库，例如{"defaultCustomLibraries": ["U%2Fconfluence%2Fdownload%2Fattachments%2F720900%2FScratchpad.xml%3Fapi%3Dv2"]}。 

  - 注意：要编码URL，请将URL输入我们的URL编码工具并选择URL编码。 要加载上面libraries部分的库，请使用defaultLibraries设置。

- enableCustomLibraries: 指定是否启用打开和新建库的功能（true或false，默认值为true）。
- templateFile: 定义模板对话框的源文件的URL（允许多个<template>标签）。 注意：如果通过代理服务器下载此文件，并使用cors URL参数（9.2.5及更高版本），则需要XML类型声明。

```
<?xml version="1.0"?>
<templates><template section="Title" url="http://example.com/diagram.xml" title="Diagram" preview="https://example.com/diagram.png" libs="general"/></templates>
```

- css: 定义一个包含CSS规则的字符串，用于配置季华绘图用户界面。例如，要更改菜单栏的背景颜色，请使用以下内容：{"css": ".geMenubarContainer { background-color: #c0c0c0 !important; } .geMenubar { background-color: #c0c0c0 !important; }"}（6.5.2及更高版本）。
- fontCss: 定义用于图表中的Web字体的CSS规则字符串。这应该是一个或多个@font-face规则，例如，要使用附加到Confluence页面上的字体文件：{"fontCss": "@font-face { font-family: 'Marvel'; src: url(/confluence/download/attachments/720900/Marvel-Regular.ttf?api=v2) format('truetype')}"} 此部分中的字体用于在编辑器中显示图表和在Google Chrome、Firefox和Microsoft Edge中创建图像。所有其他浏览器都需要在服务器端安装字体。要在浏览器中创建图像，字体必须位于同一域中并包含CORS头，否则将通过Confluence服务器进行代理。 Confluence服务器和数据中心：在Confluence管理区域的外观部分下的样式表中的全局样式表用于查看页面中的图表并从灯箱中打印图表。在这种情况下，它应该与fontCss匹配，并具有以下规则：

![Configure COnfluence Server to use fontCss rules in 季华绘图](https://www.drawio.com/assets/img/blog/configure-font-stylesheet-confluence-server.png)
Confluence Cloud: 字体URL必须是公开的，并且必须允许季华绘图来源的访问（CORS头)：
`"fontCss": "@font-face { font-family: 'Waltograph'; src: url(https://fontlibrary.org/assets/fonts/waltograph/23a40698cd1bb84f930b7a0884c134a6/ab260a56f2b852b78f81eac337e0a2fc/WaltographRegular.otf) format('opentype')}" and "customFonts": ["Waltograph”]`
**注意：**所有字体都将在客户端创建图像并保存图表时下载，因此应尽量减少自定义字体的数量。目前，外部图像服务不支持自定义字体。

- `thumbWidth/thumbHeight`: 定义左侧面板中条目的宽度和高度（6.5.4及更高版本）。
- `sidebarWidth`: 指定侧边栏的初始宽度。
- `updateDefaultStyle`: 是否在更改样式时更新默认样式。默认值为true。
- `sidebarTitles`: 指定是否显示侧边栏中的标题。默认值为false。
- `sidebarTitleSize`: 指定侧边栏标题的字体大小（以pt为单位）。默认值为8。
- `zoomWheel`: 指定是否使用鼠标滚轮进行缩放，无需任何修改键（true/false，15.0.6及更高版本）。默认值为false。
- `zoomFactor`: 定义鼠标滚轮和触控板缩放的缩放因子。默认值为1.2（14.7.0及更高版本）。
- `darkColor`: 定义暗模式的背景颜色。默认值为#2A2A2A。
- `lightColor`: 定义暗模式的前景颜色。默认值为#F0F0F0。
- `pageFormat`: 定义默认页面格式，例如对于DIN A3，可以使用`"pageFormat": {"width": 1169, "height": 1654}`，其中宽度和高度以英寸*10为单位（15.0.0及更高版本）。
- `gridSteps`: 定义次要网格步长的数量（14.3.2及更高版本）。
- `simpleLabels`: true - 默认情况下禁用标签的换行和复杂格式，以避免在SVG输出中使用foreignObjects（14.5.9及更高版本）。
- `emptyDiagramXml/emptyLibraryXml`: 定义空白图表和库的XML（6.5.4及更高版本）。

- defaultEdgeLength: 定义新连接器的默认长度（7.2.4及更高版本）。
- defaultPageVisible: 定义页面是否初始可见（true/false）。
- defaultGridEnabled: 定义网格是否初始启用（true/false）。
- autosaveDelay: 定义文件在最后更改和自动保存之间的延迟时间（以毫秒为单位）（10.4.7及更高版本）。
- version: 配置的当前版本（任意字符串，例如"1.0"）。如果与上次使用的版本不同，则会重置客户端上的当前设置（.drawio-config）。默认值为null。更改此值将强制重置客户端中存储的设置，并应用当前配置（7.2.8及更高版本）。
- override: 如果设置为true，则忽略客户端上的当前设置（9.2.5及更高版本）。
- globalVars: 使用键值对的JSON结构定义系统范围占位符的全局变量。请保持全局变量的数量较少。
- compressXml: 指定是否压缩XML输出。默认值为false。
- includeDiagram: 指定导出对话框中包括图表数据的默认设置（15.0.4及更高版本）。
- dataGovernance: 设置服务器端点区域。默认情况下，使用最近的区域（欧盟或美国）。如果lockdown设置为true，则忽略dataGovernance。
- lockdown: 禁用除直接在浏览器和选择的数据存储位置之间进行的数据传输。默认值为false。
- restrictExport: 禁用将图表导出为其他格式，但这并不阻止用户获取图表的文本或图像格式，只是相对困难一些。默认值为false。
- maxImageBytes: 定义图像的最大大小（以字节为单位）。默认值为1000000。
- maxImageSize: 定义图像的最大宽度或高度，取最低值。默认值为520。
- oneDriveInlinePicker: 指定是否使用OneDrive的内联选择器。如果未使用inlinePicker URL参数，则默认为true。
- settingsName: 指定用于存储用户设置的名称，通常在嵌入模式下，在本地存储中形式为.{name}-config。
- shareCursorPosition: 指定实时协作中共享光标的默认值。默认值为true。
- showRemoteCursors: 指定实时协作中显示远程光标的默认值。默认值为true。
- enableCssDarkMode: 指定是否应使用CSS进行暗模式。默认值为true。

## 额外的Confluence Server和Data Center选项：

- inplaceedits：如果设置为false，则禁用从查看器启动图表编辑器的能力。默认值为true（8.3.13及更高版本）。

- forceSimpleViewer：如果设置为true，则强制对每个图表使用简单的图表查看器。默认值为false（8.4.0及更高版本）。

- debug：设置为true以启用调试输出。

- defaultMacroParameters：使用JSON结构定义默认宏参数的覆盖（9.2.5及更高版本）。

  - border：布尔值。如果设置为true，则在查看器周围显示边框，默认值为true。

  - width：整数。查看器的默认宽度，默认为空白。

  - lightbox：布尔值。如果设置为true，则启用灯箱（大型查看器），默认值为true。

  - simpleViewer：布尔值。如果设置为true，则显示简单的查看器， 默认值为false。

  - toolbarStyle：字符串。默认值为“top”，可接受的值为：

    - "top"：在鼠标悬停时在查看器元素上方显示工具栏。

    - "inline"：在鼠标悬停时在查看器元素内部显示工具栏。

    - "hidden"：隐藏工具栏。

  - links：字符串。默认值为“auto”，可接受的值为：

    - "auto"：在当前窗口中打开本地链接，在新窗口中打开外部链接。

    - "blank"：在新窗口中打开所有链接。

    - "self"：在当前窗口中打开所有链接。

注意：Confluence Server或Data Center上不可用图表编辑器插件。

## Confluence Cloud的其他选项

- `ui`：定义一个字符串，包含用户界面的主题名称。可以选择以下其中一个主题：`kennedy`、`atlas`（默认）、`dark`和`min`。

## 以下是Quip的其他选项：

- `mathematicalTypesetting`：切换数学排版功能，使用MathJax加载来自math.diagrams.net的JavaScript和字体，并使用exp.diagrams.net创建图像（`true`或`false`，默认为`true`）。
- `internationalization`：切换`i18n`功能，使用app.diagrams.net的资源（`true`或`false`，默认为`true`）。如果禁用此功能，Quip实时应用程序的用户界面将仅显示为英文。
- `iconfinder`：在左侧面板搜索框中切换使用Iconfinder搜索形状。
- `plantUml`：切换插入PlantUML标记的功能，使用`exp-plant.diagrams.net`（`true`或`false`，默认为`true`）。
- `exportPdf`：切换导出为PDF文件的功能，使用`exp.diagrams.net`（`true`或`false`，默认为`true`）。
- `remoteConvert`：切换转换需要远程连接的文件的功能，包括Gliffy、.vsd和.vss文件（`true`或`false`，默认为`true`）。
- `password`：使用可选字符串保护对站点配置的访问（只允许站点管理员访问）。
- `maxHistoryDays`：指定保留编辑历史记录的天数。默认为`14`。如果上次编辑时间早于这个天数，编辑开始时会清除历史记录。可以使用“首选项>压缩”手动清除历史记录。
- `debug`：切换浏览器控制台中的调试输出（`true`或`false`，默认为`false`）。

如果这些选项在您的配置中不可见，请单击“重置”以恢复默认值。

如果所有以上选项都被禁用，则Quip的季华绘图将不会使用任何外部资源或服务（除了来自app.diagrams.net的图像）。

“首选项”对话框中的“高级”按钮仅对Quip站点管理员可见。

Quip中配置的最大允许大小为10 kB。

## 示例：

以下是具有默认值的JSON字符串示例（如果变量被省略）：

```
{ "defaultFonts": ["Helvetica", "Verdana", "Times New Roman", "Garamond", "Comic Sans MS", "Courier New", "Georgia", "Lucida Console", "Tahoma"],
  "presetColors": ["E6D0DE", "CDA2BE", "B5739D", "E1D5E7", "C3ABD0", "A680B8", "D4E1F5", "A9C4EB", "7EA6E0", "D5E8D4", "9AC7BF", "67AB9F", "D5E8D4", "B9E0A5", "97D077", "FFF2CC", "FFE599", "FFD966", "FFF4C3", "FFCE9F", "FFB570", "F8CECC", "F19C99", "EA6B66"],
  "defaultColorSchemes": [
  [ null, { "fill": "#f5f5f5", "stroke": "#666666" },
     {	"fill": "#dae8fc", "stroke": "#6c8ebf" },
     {	"fill": "#d5e8d4", "stroke": "#82b366" },
     {	"fill": "#ffe6cc", "stroke": "#d79b00" },
     {	"fill": "#fff2cc", "stroke": "#d6b656" },
     { "fill": "#f8cecc", "stroke": "#b85450" },
     {	"fill": "#e1d5e7", "stroke": "#9673a6" }],
	[ null, { "fill": "#f5f5f5", "stroke": "#666666", "gradient": "#b3b3b3" },
     {	"fill": "#dae8fc", "stroke": "#6c8ebf",	"gradient": "#7ea6e0" },
     {	"fill": "#d5e8d4", "stroke": "#82b366",	"gradient": "#97d077" },
     {	"fill": "#ffcd28", "stroke": "#d79b00",	"gradient": "#ffa500" },
     {	"fill": "#fff2cc", "stroke": "#d6b656",	"gradient": "#ffd966" },
     {	"fill": "#f8cecc", "stroke": "#b85450",	"gradient": "#ea6b66" },
     {	"fill": "#e6d0de", "stroke": "#996185",	"gradient": "#d5739d" }],
	[ null, { "fill": "#eeeeee", "stroke": "#36393d" },
     {	"fill": "#f9f7ed", "stroke": "#36393d" },
     {	"fill": "#ffcc99", "stroke": "#36393d" },
     {	"fill": "#cce5ff", "stroke": "#36393d" },
     {	"fill": "#ffff88", "stroke": "#36393d" },
     {	"fill": "#cdeb8b", "stroke": "#36393d" },
     {	"fill": "#ffcccc", "stroke": "#36393d" }]
	],
  "defaultColors": ["none", "FFFFFF", "E6E6E6", "CCCCCC", "B3B3B3", "999999", "808080", "666666", "4D4D4D", "333333", "1A1A1A", "000000", "FFCCCC", "FFE6CC", "FFFFCC", "E6FFCC", "CCFFCC", "CCFFE6", "CCFFFF", "CCE5FF", "CCCCFF", "E5CCFF", "FFCCFF", "FFCCE6", "FF9999", "FFCC99", "FFFF99", "CCFF99", "99FF99", "99FFCC", "99FFFF", "99CCFF", "9999FF", "CC99FF", "FF99FF", "FF99CC", "FF6666", "FFB366", "FFFF66", "B3FF66", "66FF66", "66FFB3", "66FFFF", "66B2FF", "6666FF", "B266FF", "FF66FF", "FF66B3", "FF3333", "FF9933", "FFFF33", "99FF33", "33FF33", "33FF99", "33FFFF", "3399FF", "3333FF", "9933FF", "FF33FF", "FF3399", "FF0000", "FF8000", "FFFF00", "80FF00", "00FF00", "00FF80", "00FFFF", "007FFF", "0000FF", "7F00FF", "FF00FF", "FF0080", "CC0000", "CC6600", "CCCC00", "66CC00", "00CC00", "00CC66", "00CCCC", "0066CC", "0000CC", "6600CC", "CC00CC", "CC0066", "990000", "994C00", "999900", "4D9900", "009900", "00994D", "009999", "004C99", "000099", "4C0099", "990099", "99004D", "660000", "663300", "666600", "336600", "006600", "006633", "006666", "003366", "000066", "330066", "660066", "660033", "330000", "331A00", "333300", "1A3300", "003300", "00331A", "003333", "001933", "000033", "190033", "330033", "33001A"],
	"defaultVertexStyle": {},
	"defaultEdgeStyle": {
		"edgeStyle": "orthogonalEdgeStyle",
		"rounded": "0",
		"jettySize": "auto",
		"orthogonalLoop": "1" },
	"defaultLibraries": "general;images;uml;er;bpmn;flowchart;basic;arrows2",
	"defaultCustomLibraries": [],
	"defaultMacroParameters": {
		"border": false,
		"toolbarStyle": "inline" },
	"css": "",
	"fontCss": "",
	"thumbWidth": 46,
	"thumbHeight": 46,
	"emptyDiagramXml": "<mxGraphModel><root><mxCell id='0'/><mxCell id='1' parent='0'/></root></mxGraphModel>",
	"emptyLibraryXml": "<mxlibrary>[]</mxlibrary>",
	"defaultEdgeLength": 80 }
```

在线版本的配置存储在您的浏览器的本地存储中，键名为`.configuration`。

![The 季华绘图 configuration is stored in your browser's local storage](https://www.drawio.com/assets/img/blog/configuration-browser-local-storage.png)

当前编辑器的设置（例如最近使用的颜色、当前打开的库等）在您的浏览器的本地存储中，键名为`.drawio-config`，以持久保存。

![Current settings for 季华绘图 are saved in local storage in your browser](https://www.drawio.com/assets/img/blog/current-settings-local-storage-browser.png)

您可以直接将defaultEdgeLength和autosaveDelay添加到.drawio-config中，以覆盖浏览器中Web应用程序的默认值。

## 要删除当前设置或配置，请按照以下步骤操作：

1. 打开Google Chrome开发者工具：更多工具 > 开发者工具。
2. 切换到“应用程序”选项卡，并选择“存储” > “本地存储” > “your_domain_name”。
3. 在键值表中，右键单击并删除`.drawio-config`。

## 修复配置中的错误

如果配置文件格式无效，当图表编辑器打开时，Chrome控制台选项卡会显示配置错误。请将双重转义的引号（\”）替换为单重转义的引号（"），以确保配置是有效的JSON格式，并可以使用JSONLint等验证器进行检查。

这样做可以确保配置文件的格式正确，并且可以通过验证器（如JSONLint）进行检查。

## 配置在线应用程序

您可以通过点击“配置”对话框中的“链接”来配置季华绘图在线应用程序：点击“帮助 > 配置”。

注意：如果您需要支持Microsoft Edge或IE11，则必须确保哈希值不超过2,025个字符。