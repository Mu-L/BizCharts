# 圆角柱状图(BizCharts@4)

![预览](http://bizcharts-resource.oss-cn-zhangjiakou.aliyuncs.com/images/d43ea040-bf7e-11ea-95ad-696ab6ed1a1c.png)

```js
import React from "react";
import {
  Chart,
  Tooltip,
  Interval,
  Annotation,
  Axis,
  registerShape
} from "bizcharts";


registerShape('interval', 'border-radius', {
  draw(cfg, container) {
    const { points } = cfg;
    let path = [];
    path.push(['M', points[0].x, points[0].y]);
    path.push(['L', points[1].x, points[1].y]);
    path.push(['L', points[2].x, points[2].y]);
    path.push(['L', points[3].x, points[3].y]);
    path.push('Z');
    path = this.parsePath(path); // 将 0 - 1 转化为画布坐标

    const group = container.addGroup();
    group.addShape('rect', {
      attrs: {
        x: path[1][1], // 矩形起始点为左上角
        y: path[1][2],
        width: path[2][1] - path[1][1],
        height: path[0][2] - path[1][2],
        fill: cfg.color,
        radius: (path[2][1] - path[1][1]) / 2,
      },
    });

    return group;
  },
});

const activeData = [
  { date: '2017年3月2日', actual: 175, expected: 900 },
  { date: '2017年3月3日', actual: 137, expected: 900 },
  { date: '2017年3月4日', actual: 240, expected: 900 },
  { date: '2017年3月5日', actual: 726, expected: 900 },
  { date: '2017年3月6日', actual: 968, expected: 900 },
  { date: '2017年3月7日', actual: 702, expected: 900 },
  { date: '2017年3月8日', actual: 655, expected: 900 },
  { date: '2017年3月9日', actual: 463, expected: 900 },
  { date: '2017年3月10日', actual: 464, expected: 900 },
  { date: '2017年3月12日', actual: 0, expected: 900 },
  { date: '2017年3月13日', actual: 638, expected: 900 },
  { date: '2017年3月14日', actual: 0, expected: 900 },
  { date: '2017年3月15日', actual: 0, expected: 900 },
  { date: '2017年3月16日', actual: 509, expected: 900 },
  { date: '2017年3月17日', actual: 269, expected: 900 },
  { date: '2017年3月18日', actual: 321, expected: 900 },
  { date: '2017年3月19日', actual: 0, expected: 900 },
  { date: '2017年3月20日', actual: 399, expected: 900 },
  { date: '2017年3月21日', actual: 662, expected: 900 },
  { date: '2017年3月22日', actual: 689, expected: 900 },
  { date: '2017年3月23日', actual: 347, expected: 900 },
  { date: '2017年3月24日', actual: 0, expected: 900 },
  { date: '2017年3月26日', actual: 428, expected: 900 },
  { date: '2017年3月27日', actual: 749, expected: 900 },
  { date: '2017年3月28日', actual: 0, expected: 900 },
  { date: '2017年3月29日', actual: 0, expected: 900 },
  { date: '2017年3月30日', actual: 69.1, expected: 900 },
];

function Demo() {
  const scale = {
    expected: {
      min: 0,
      max: 1000,
      sync: 'value',
    },
    actual: {
      sync: 'value',
    },
  };
  return (
    <Chart height={400} scale={scale} padding="auto" data={activeData} autoFit>
      <Interval
        color="#cbcbcb"
        shape="border-radius"
        position="date*expected"
      />
      <Interval
        position="date*actual"
        color="#5B8FF9"
        shape={['date*actual', (date, val) => {
          if (val === 0) {
            return;
          }
          // eslint-disable-next-line consistent-return
          return 'border-radius';
        }]}
      />
      <Axis name="actual" visible={false} />
      <Axis name="date" visible={false} />
      <Axis
        name="expected"
        position="right"
        line={false}
        tickLine={false}
        label={{
          formatter: (val) => {
            if (val === '1200') {
              return '';
            }
            return val;
          },
        }}
      />
      <Annotation.Text
        position={['max', 'max']}
        offsetY={10}
        content="67 / 900 千卡"
        style={{
          fill: '#cbcbcb',
          fontSize: 20,
          textAlign: 'end',
          textBaseline: 'top',
        }}
      />
      <Annotation.Text
        position={['min', 'max']}
        offsetY={10}
        content="活动"
        style={{
          fill: '#5B8FF9',
          fontSize: 20,
          fontWeight: 'bold',
          textBaseline: 'top',
        }}
      />
      <Tooltip shared />
    </Chart>
  );
}

ReactDOM.render(<Demo />, mountNode)

```
