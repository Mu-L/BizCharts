# 南丁格尔玫瑰环图(BizCharts@4)

![预览](http://bizcharts-resource.oss-cn-zhangjiakou.aliyuncs.com/images/e0fc11d0-9979-11ea-8225-e30c1937e15c.png)

```js
import React from 'react';
import {
  Chart,
  Interval,
  Tooltip,
  Axis,
  Coordinate
} from 'bizcharts';

function Labelline () {
  const data = [
    { year: '2001', population: 41.8 },
    { year: '2002', population: 38 },
    { year: '2003', population: 33.7 },
    { year: '2004', population: 30.7 },
    { year: '2005', population: 25.8 },
    { year: '2006', population: 31.7 },
    { year: '2007', population: 33 },
    { year: '2008', population: 46 },
    { year: '2009', population: 38.3 },
    { year: '2010', population: 28 },
    { year: '2011', population: 42.5 },
    { year: '2012', population: 30.3 },
  ];


  return (
    <Chart height={400} data={data} autoFit>
      <Coordinate type="polar" innerRadius={0.2} />
      <Axis visible={false} />
      <Tooltip showTitle={false} />
      <Interval
        position="year*population"
        adjust="stack"
        color="year"
        element-highlight
        style={{
          lineWidth: 1,
          stroke: '#fff',
        }}
        label={['year', {
           offset: -15,
        }]}
      />
    </Chart>
  );
}

ReactDOM.render(<Labelline />, mountNode);

```
