# DonutChart

环图，甜甜圈图

环图与饼图基本功能类似，用于比较整体和部分的关系，每个弧形切片表示整体中的一个分类。由饼图挖空中心部分构成，通常在中心部分会放置解释性文本。

## 使用
解构使用
```js
import { DonutChart } from 'bizcharts';
function APP() {
  return <DonutChart {...options} />;
}
```
按需使用
```js
import DonutChart from 'bizcharts/lib/plots/DonutChart'; // es 取 'bizcharts/es/plots/DonutChart'
function APP() {
  return <DonutChart {...options} />;
}
```

## API

### width

**可选**, _<number>_

功能描述： 设置图表宽度。

默认配置： `400`

### height

**可选**, _<number>_

功能描述： 设置图表高度。

默认配置： `400`

### forceFit

**可选**, _<boolean>_

功能描述： 图表是否自适应容器宽高。当 `forceFit` 设置为true时，`width` 和 `height` 的设置将失效。

默认配置： `true`

### pixelRatio

**可选**, _<number>_

功能描述： 设置图表渲染的像素比

默认配置： `2`

### renderer

**可选**, _<string>_

功能描述: 设置图表渲染方式为 `canvas` 或 `svg`

默认配置： `canvas`

## 数据映射

### data 

**必选**, _<array>_ _<object>_

功能描述： 设置图表数据源

默认配置： 无

数据源为对象集合，例如：`[{ type: 'a'，value: 20 }, { type: 'b'，value: 20 }]`。

### meta
**可选**, _<object>_

功能描述： 全局化配置图表数据元信息，以字段为单位进行配置。在 meta 上的配置将同时影响所有组件的文本信息。

默认配置： 无

| 细分配置项名称 | 类型 | 功能描述 |
| --- | --- | --- |
| alias | *string* | 字段的别名 |
| formatter | *function* | callback方法，对该字段所有值进行格式化处理 |
| values | *string[]* | 枚举该字段下所有值 |
| range | *number[]* | 字段的数据映射区间，默认为[0,1] |


```js
const data = [
  { country: 'Asia', year: '1750', value: 502,},
  { country: 'Asia', year: '1800', value: 635,},
  { country: 'Europe', year: '1750', value: 163,},
  { country: 'Europe', year: '1800', value: 203,},
];

<DonutChart
  data={data}
  title={{
    visible: true,
  }}
  meta={{
    year: {
      alias:'年份'
      range: [0, 1],
    },
    value: {
      alias: '数量',
      formatter:(v)=>{return `${v}个`}
    }
  }}
  // highlight-end
  angleField="year"
/>

```

### angleField ✨
**必选**, _<string>_

功能描述： 扇形切片大小（弧度）所对应的数据字段名。。

默认配置： 无

### colorField ✨
**可选**, _<string>_

功能描述：扇形颜色映射对应的数据字段名。

默认配置： 无

## 图形样式

### radius ✨
**可选**, _<number>_

功能描述： 环图的半径，原点为画布中心。配置值域为 [0,1]，0 代表环图大小为 0，即不显示，1 代表环图撑满绘图区域。

默认配置： 0.8, 即 width / 2 * 0.8。


### innerRadius ✨
**可选**, _<number>_

功能描述： 环图的内环半径，原点为画布中心。半径和内环半径决定了环图的厚度 (thickness)。

默认配置： 0.8


### color
**可选**, _<string>_ | _<string[]>_ | _<Function>_

功能描述： 指定扇形颜色，即可以指定一系列色值，也可以通过回调函数的方法根据对应数值进行设置。

默认配置：采用 theme 中的色板。

用法示例：

```js
// 配合颜色映射，指定多值
colorField:'type',
color:['blue','yellow','green']
//配合颜色映射，使用回调函数指定色值
colorField:'type',
color:(d)=>{
    if(d==='a') return 'red';
    return 'blue';
}
```

### pieStyle ✨
**可选**, _<object>_

功能描述： 设置扇形样式。ringStyle中的`fill`会覆盖 `color` 的配置。ringStyle可以直接指定，也可以通过callback的方式，根据数据为每个扇形切片指定单独的样式。

默认配置： 无


| 细分配置 | 类型 | 功能描述 |
| --- | --- | --- |
| fill | string | 填充颜色 |
| stroke | string | 描边颜色 |
| lineWidth | number | 描边宽度 |
| lineDash | number | 虚线描边 |
| opacity | number | 整体透明度 |
| fillOpacity | number | 填充透明度 |
| strokeOpacity | number | 描边透明度 |

## 图表组件

<img src="https://gw.alipayobjects.com/mdn/rms_d314dd/afts/img/A*P_fkQpeVHVUAAAAAAAAAAABkARQnAQ" width="600">

### title
**可选**, _<optional>_


功能描述： 配置图表的标题，默认显示在图表左上角。

| 细分配置 | 类型 | 功能描述 | 默认配置 |
| --- | --- | --- | --- |
| visible | boolean | 是否显示 | false |
| text | string | 图表的标题文本 | - |
| alignTo | string | 位置，支持三种配置：<br />'left','middle','right' | left |
| style | object | 样式：<br />- fontSize: number 文字大小<br />- fill: string 文字颜色<br />- stroke: string  描边颜色<br />- lineWidth: number 描边粗细<br />- lineDash: number 虚线描边<br />- opacity: number 透明度<br />- fillOpacity: number 填充透明度<br />- strokeOpacity: number 描边透明度<br /> | `{ fontSize: 18, fill: 'black' }` |

### description
**可选**, _<optional>_


功能描述： 配置图表的描述，默认显示在图表左上角，标题下方。

| 细分配置 | 类型 | 功能描述 | 默认配置 |
| --- | --- | --- | --- |
| visible | boolean | 是否显示 | false |
| text | string | 图表的描述文本 | - |
| alignTo | string | 位置，支持三种配置：<br />'left','middle','right' | left |
| style | object | 样式：<br />- fontSize: number 文字大小<br />- fill: string 文字颜色<br />- stroke: string  描边颜色<br />- lineWidth: number 描边粗细<br />- lineDash: number 虚线描边<br />- opacity: number 透明度<br />- fillOpacity: number 填充透明度<br />- strokeOpacity: number 描边透明度<br /> | `{ fontSize: 12, fill: 'grey' }` |

### legend
**可选**, _<object>_


功能描述：图例，配置colorField时显示，用于展示颜色分类信息

| 细分配置 | 类型 | 功能描述 |
| --- | --- | --- |
| visible | boolean | 是否可见 |
| position | string | 位置，支持12方位布局<br />top-left, top-center,top-right<br />bottom-left,bottom-center,bottom-right<br />left-top,left-center,left-bottom<br />right-top,right-center,right-bottom |
| formatter | function | 对图例显示信息进行格式化 |
| offsetX | number | 图例在 position 的基础上再往 x 方向偏移量，单位 px |
| offestY | number | 图例在 position 的基础上再往 y 方向偏移量，单位 px |
| title | object | 图例标题<br />- visible: boolean 是否显示<br />- text: string 图例文本，如不配置则自动取对应字段名<br />- style: object 标题样式<br /> |
| marker | object | 图例 marker<br />- symbol: string marker符号，默认为 'circle'。可选类型：circle,square,diamond,triangle,triangleDown,hexagon,bowtie,cross,tick,plus,hyphen,line,hollowCircle,hollowSquare,hollowDiamond<br />- style: object marker样式，其中 `r` 配置marker的大小，其余样式参数参考绘图属性文档。<br /> |
| text | object | 图例文本<br />- style: object 配置图例文本样式<br />- formatter:(text,cfg)=>string 格式化图例文本<br /> |

### tooltip
**可选**, _<object>_

功能描述：信息提示框

| 细分属性 | 类型 | 功能描述 | 默认配置 |
| --- | --- | --- | --- |
| visible | boolean | 是否显示 | true |
| offset | number | 距离鼠标位置偏移值 | 20 |
| domStyles | object | 配置tooltip样式<br />- g2-tooltip: object 设置tooltip容器的CSS样式<br />- g2-tooltip-title: object 设置tooltip标题的CSS样式<br />- g2-tooltip-list: object 设置tooltip列表容器的CSS 样式<br />- g2-tooltip-marker: object 设置tooltip列表容器中每一项 marker的CSS样式<br />- g2-tooltip-value: object 设置tooltip 列表容器中每一项 value的CSS样式<br /> | - |
| fields | string | 设置tooltip内容字段，默认为[ `angleField`,`colorField`] |
| formatter | object | 对tooltip items进行格式化，入参为tooltip fields对应数值，出参为格式为{name:'a',value:1} |

### label
**可选**, _<object>_

功能描述： 标签文本

| 细分配置 | 类型 | 功能描述 | 默认配置 |
| --- | --- | --- | --- |
| visible | boolean | 是否显示 | false |
| type | string | label的类型<br />- inner label显示于扇形切片内<br />- outer label显示于饼外<br />- outer-center label呈圆形排布于饼外<br />- spider 蜘蛛布局label| inner |
| autoRotate | boolean | 是否自动旋转 | false |
| formatter | function | 对文本标签内容进行格式化 | - |
| offsetX | number | 在 label 位置的基础上再往 x 方向的偏移量 | - |
| offsetY | number | 在 label 位置的基础上再往 y 方向的偏移量 | - |
| style | object | 配置文本标签样式。 | - |

<img src="https://gw.alipayobjects.com/mdn/rms_d314dd/afts/img/A*TeCBRbMLDKsAAAAAAAAAAABkARQnAQ" alt="image.png" style="visibility: visible; width: 800px; height: 248px;">

spider label formatter用法示例：

当配置了 colorField，即扇形切片接受分类类型的颜色映射，此时 spider label 的文本为上下显示，此时 formatter 方法入参为 angleField 及 colorField 两个字段对应的值，返回值应为数组。

```js
label: {
  type: 'spider',
  formatter: (angleField, colorField) => {
    return [ 'value1','value2' ];
  }
}
```

### statistic ✨

**可选**, _<object>_

功能描述：统计内容组件。当内半径(innerRadius) 大于 0 时才生效，默认展示汇总值，可以通过 formatter 格式化展示内容，也可以通过 customHtml 自定义更多的内容。

| 配置项 | 类型 | 描述 |
| --- | --- | --- |
| title | false 或者 StatisticText | 标题|
| content | false 或者 StatisticText | 主体内容 | - |

StatisticText
| 配置项 | 类型 | 
| --- | --- | 
| style | CSSStyleDeclaration |
| customHtml | (container: HTMLElement, view: View, datum: object, data: object[]) => string; | 
| formatter | Function |
| rotate | number |
| offsetX | number |
| offsetY | number |

## 事件 events

使用说明：
```js
<DonutChart
    events={{
        onRingClick: (event) => console.log(event),
        onLegendClick: (event) => console.log(event),
        onPlotClick: (event) => console.log(event),
    }}
/>
```

### 图形事件

| onRingClick<br />图形点击事件 | onRingDblClick<br />图形双击事件 | onRingDblClick<br />图形双击事件 | onRingMouseleave<br />图形鼠标离开事件 |
| --- | --- | --- | --- |
| onRingMousemove<br />图形鼠标移动事件 | onRingMousedown<br />图形鼠标按下事件 | onRingMouseup<br />图形鼠标松开事件 | onRingMouseenter<br />图形鼠标进入事件 |


### 图表区域事件

| onPlotClick<br />图表区域点击事件 | onPlotDblClick<br />图表区域双击事件 | onPlotDblClick<br />图表区域双击事件 | onPlotMouseleave<br />图表区域鼠标离开事件 |
| --- | --- | --- | --- |
| onPlotMousemove<br />图表区域鼠标移动事件 | onPlotMousedown<br />图表区域鼠标按下事件 | onPlotMouseup<br />图表区域鼠标松开事件 | onPlotMouseenter<br />图表区域鼠标进入事件 |


### 图例事件

| onLegendClick<br />图例点击事件 | onLegendDblClick<br />图例双击事件 | onLegendMouseenter<br />图例鼠标进入事件 | onLegendMouseleave<br />图例鼠标离开事件 |
| --- | --- | --- | --- |
| onLegendMousemove<br />图例鼠标移动事件 | onLegendMousedown<br />图例鼠标按下事件 | onLegendMouseup<br />图例鼠标松开事件 | onLegendMouseenter<br />图例鼠标进入事件 |


### 图形标签事件

| onLabelClick<br />图形标签点击事件 | onLabelDblClick<br />图形标签双击事件 | onLabelDblClick<br />图形标签双击事件 | onLabelMouseleave<br />图形标签鼠标离开事件 |
| --- | --- | --- | --- |
| onLabelMousemove<br />图形标签鼠标移动事件 | onLabelMousedown<br />图形标签鼠标按下事件 | onLabelMouseup<br />图形标签鼠标松开事件 | onLabelMouseenter<br />图形标签鼠标进入事件 |


### 标题事件

| onTitleClick<br />标题点击事件 | onTitleDblClick<br />标题双击事件 | onTitleDblClick<br />标题双击事件 | onTitleMouseleave<br />标题鼠标离开事件 |
| --- | --- | --- | --- |
| onTitleMousemove<br />标题鼠标移动事件 | onTitleMousedown<br />标题鼠标按下事件 | onTitleMouseup<br />标题鼠标松开事件 | onTitleMouseenter<br />标题鼠标进入事件 |


### 描述事件

| onDescriptionClick<br />标题点击事件 | onDescriptionDblClick<br />标题双击事件 | onDescriptionDblClick<br />标题双击事件 | onDescriptionMouseleave<br />标题鼠标离开事件 |
| --- | --- | --- | --- |
| onDescriptionMousemove<br />标题鼠标移动事件 | onDescriptionMousedown<br />标题鼠标按下事件 | onDescriptionMouseup<br />标题鼠标松开事件 | onDescriptionMouseenter<br />标题鼠标进入事件 |
