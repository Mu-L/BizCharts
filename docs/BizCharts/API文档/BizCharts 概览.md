# BizCharts 概览

> 如果是 umd 文件引入

```js
BizCharts = Window.BizCharts;
```
> 如果是 package 引入，BizCharts 为:

```js
import * as BizCharts from "bizcharts";
```

全局命名空间 BizCharts 包含：

## 组件

#### Chart
图表最顶级的组件，控制着图表的创建、绘制、销毁等。
详细文档见 [Chart api](24)

#### Coord
坐标系组件，设置 Chart 或者 View 的坐标系类型。
详细文档见 [Coord api](25)

#### Axis
坐标轴组件，控制图表中坐标轴的样式等。
详细文档见 [Axis api](26)

#### Geom
几何标记对象，决定创建图表的类型。
详细文档见 [Geom api](27)。

#### Label
几何标记对象上的文本。
详细文档见 [Label api](28)

#### Legend
图例。
详细文档见 [Legend api](29)

#### Guide
坐标轴组件，控制图表中坐标轴的样式等。
详细文档见 [Guide api](31)

#### Facet
控制 Chart 分面。
详细文档见 [Facet api](32)

#### View
视图组件。
详细文档见 [View api](33)

<span id="G2" />
## G2
G2 的命名空间，在有需要的情况下用户可以直接拿到该对象去工作。

<span id="Animate" />
## Animate
用来注册用户自定义动画。
详细文档见 [动画教程](../../12/page/22)。

<span id="Shape" />
## Shape
构成图表具体的形状类。
详细文档见 [Shape api](36)。

<span id="setTheme" />
## setTheme
设置 BizCharts 中使用的主题类型。
详细文档见 [theme tutorial](41)。

<span id="track" />
## track
该方法用于 G2 情况的打点监控，默认处于开启状态，如果您不想让我们知道您的版本使用情况，请配置为 false。
```js
BizCharts.track(false);
```
<span id="PathUtil" />
## PathUtil
来自 G2，用于操作图形路径的工具类。具体提供的方法如下：

| 方法                                            | 参数说明                                                                                 | 返回结果                                                                      |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `getBoundingClientRect(node)`                   | `node`:HTMLElement，dom 节点                                                             | 返回该节点在页面中的位置，返回结果格式为： `{top: , bottom: , left: , right}` |
| `getStyle(dom, name)`                           | `dom`:HTMLElement，DOM 节点；`name`:String，样式名                                       | 返回该节点对应样式名 name 的具体样式。                                        |
| `modifyCSS(dom, css)`                           | `dom`:HTMLElement，DOM 节点；`css`:Object，样式属性                                      | 修改对应节点的 css 样式，返回修改样式后的 dom 对象。                          |
| `createDom(str)`                                | `str`:String，Dom 字符串                                                                 | 按照传入的 str 创建 dom 节点，并返回创建的节点。                              |
| `getRatio()`                                    | --                                                                                       | 返回屏幕的像素分辨率。                                                        |
| `getWidth(el)`                                  | `el`:HTMLElement，dom 节点                                                               | 返回 dom 节点的宽度，不包含 padding、border                                   |
| `getHeight(el)`                                 | `e`l:HTMLElement，dom 节点                                                               | 返回 dom 节点的高度，不包含 padding、border                                   |
| `getOuterWidth(el)`                             | `el`:HTMLElement，dom 节点                                                               | 返回 dom 节点的宽度，包含 padding、border                                     |
| `getOuterHeight(el)`                            | `el`:HTMLElement，dom 节点                                                               | 返回 dom 节点的高度，包含 padding、border                                     |
| `addEventListener(target, eventType, callback)` | `target`:HTMLElement，DOM对象；`eventType`:String，事件名；`callback`:Function，回调函数 | 添加事件监听器                                                                |
| `requestAnimationFrame(fn)`                     | `fn`:Function，回调函数                                                                  | 用于定时循环操作。                                                            |

<span id="Util" />
## Util
默认提供的常见的工具类，大部分基于 lodash 封装。
如下：
```js
const Util = {
  each: require('lodash/each'),
  map: require('lodash/map'),
  isObject: require('lodash/isObject'),
  isNumber: require('lodash/isNumber'),
  isString: require('lodash/isString'),
  isFunction: require('lodash/isFunction'),
  ...
};
```

#### 绘图属性 [跳转链接](40)


