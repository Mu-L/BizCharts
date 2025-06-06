# Coord

坐标系组件。
坐标系是将两种位置标度结合在一起组成的 2 维定位系统，描述了数据是如何映射到图形所在的平面。BizCharts 将坐标系抽象为组件，并且包含两种类型坐标系极坐标系（polar、theta、helix 均属于极坐标）和笛卡尔坐标系，目前所有的坐标系均是 2 维的。

## 父组件
* [`<Chart />`](24)
* [`<View />`](33)

## 子组件
无

## 使用说明
```js
<Chart>
 <Coord type='polar' transpose={true} />
</Chart>
```
- Coord组件用来描述图表中各元素绘制时所处的坐标系，一般一个图表中只存在一个坐标系；但是[`<View />`](33)中可以有独立坐标系存在；若没有特别说明，则默认当前图表的坐标系为**直角坐标系（rect）**。

- 默认采用笛卡尔坐标系，若要改变坐标系可以通过[type](#type)属性改变。

例如下图展示的层叠柱状图，在不同坐标系下就变换成了其他的图表类型：

![image](https://zos.alipayobjects.com/skylark/fd9ba64b-b569-4c1d-acb9-d4dad3500258/attach/2378/44af7b435f0d3f88/image.png)

上图左侧为层叠柱状图，中间的饼图则是层叠柱状图在极坐标下对 x y 两个坐标轴进行转置后的结果，其中 x 轴被映射为半径，y 轴被映射成了角度。而最右边的牛眼图则相反，y 轴映射为半径。

- 极坐标默认的起始角度和结束角度如下图所示：

![image](https://zos.alipayobjects.com/skylark/85950a42-9579-44cb-b656-8dd28c9a014a/attach/2378/d648679184c6977c/image.png)


<span id="API"></span>
## API

<span id="type"></span>
### type
_<String>_
* 描述：坐标系类型;不同类型的坐标系所支持的配置属性也不一样。具体见各类型属性说明。

BizCharts 中支持的坐标系有：

| 类型 | 说明 |
|  :--  |  :--  |
| [rect](#rect) | 默认类型，直角坐标系，由 x, y 两个垂直的维度构成。 |
| [polar](#polar) | 极坐标系，由角度和半径 2 个维度构成。|
| [theta](#theta) | 一种半径固定的极坐标系，常用于饼图。 |
| [helix](#helix) | 螺旋坐标系，基于阿基米德螺旋线。|

<span id="rotate"></span>
### rotate
_<Number>_
* 描述：坐标系旋转，angle 表示旋转的度数，单位为角度。

<span id="scale"></span>
### scale
_<Array>_
* 描述：放大、缩小，默认按照坐标系中心放大、缩小。
参数为长度2的数组，第一个值代表 x 方向缩放比例，第二个值代表 y 方向缩放比例。
```js
<Coord scale={[0.7, 1.2]} />
```
![image](https://zos.alipayobjects.com/rmsportal/bAISlaEvIUpqIFVBiXKo.gif)

<span id="reflect"></span>
### reflect
* 类型：'x' | 'y' | _<Array>_
* 描述：镜像, 沿 x 方向镜像或者沿 y 轴方向映射。默认值为：'y'.
如果参数是个数组，将依次调用.例如['x', 'y'] 则先执行x方向翻转`reflect('x')` 再执行y方向翻转`reflect('y')`,以此类推。
![image](https://zos.alipayobjects.com/skylark/3e02d865-fcfc-4afd-9ffa-66a1299b31b5/attach/2378/4225fd7483f54155/image.png)

<span id="transpose"></span>
### transpose
_<Boolean>_
* 描述: 将坐标系 x 轴和 y 轴交换.

```js
 <Coord transpose={true} />
```
![image](https://img.alicdn.com/tfs/TB1yYMVopooBKNjSZPhXXc2CXXa-534-157.png)

<span id="rect"></span>
## 直角坐标系（rect）
无额外配置参数。

## 极坐标系（polar/theta/clock/gauge）
![5.png](https://img.alicdn.com/tfs/TB1nBh1vHSYBuNjSspiXXXNzpXa-1200-280.png)

<span id="polar"></span>
<span id="theta"></span>
### polar、theta 类型的极坐标系配置

| 属性名 | 说明 | 类型  | 可选值 | 默认值 |
|  :--  |  :--  |  :--  |  :--  |  :--  |
| radius | 设置半径，值为 0 至 1 的小数 | Number |  |  |
| innerRadius | 内部极坐标系的半径，[0 - 1]的小数 | Number |  |  |
| startAngle | 起始角度（弧度） | Number |  |  |
| endAngle | 结束角度（弧度） | Number |  |  | |
```js
//polar 示例
<coord type="polar" radius={0.5} startAngle={-Math.PI / 6} endAngle={7 * Math.PI /6}/>
```
效果如图：

<img src="https://gw.alipayobjects.com/zos/rmsportal/YbxpoBRuIrNsaMNOCmcG.png" width="104px">

```js
//theta 示例
<coord type="theta" innerRadius={0.5}/>
```
效果如图：

<img src="https://gw.alipayobjects.com/zos/rmsportal/xQxbzqQTjELOvrKSFEkh.png" width="100px">

<span id="gauge"></span>
### gauge 类型的极坐标系配置

| 属性名 | 说明 | 类型  | 可选值 | 默认值 |
|  :--  |  :--  |  :--  |  :--  |  :--  |
| startAngle | 起始角度（弧度） | Number |  |  |
| endAngle | 结束角度（弧度） | Number |  |  | |

<span id="clock"></span>
### clock 类型的极坐标系配置
无额外配置属性。

```js
// 这里只显示部分核心代码
<Chart width={600} height={400} data={val} scale={cols} padding={100}>
	<Coord type='gauge' startAngle={-9/8 * Math.PI} endAngle={1/8 * Math.PI} />
	<Axis name="value" />
	<Geom type="point" position="value" />
</Chart>
```

<span id="helix"></span>
## helix 螺旋坐标系配置
> 螺旋坐标系，常用于周期性数据。

对于螺旋坐标系，其可配置的参数如下：

| 属性名 | 说明 | 类型  | 可选值 | 默认值 |
|  :--  |  :--  |  :--  |  :--  |  :--  |
| radius | 设置半径，值为 0 至 1 的小数 | Number |  |  |
| startAngle | 螺旋线起点弧度 | Number |  |  |
| endAngle | 螺线线终点弧度 | Number |  |  |

```js
//示例
<Coord type="helix" startAngle={0.5 * Math.PI} endAngle={12.5 * Math.PI} radius={0.8}/>
```
效果如图：

<img src="https://gw.alipayobjects.com/zos/rmsportal/EWHCatHynDfQTPByyfVp.png" width="140px">
