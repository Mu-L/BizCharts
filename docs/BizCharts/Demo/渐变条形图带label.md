# 渐变条形图带label

![预览](http://bizcharts-resource.oss-cn-zhangjiakou.aliyuncs.com/images/77b93360-9979-11ea-bd36-0f0eda3e7ac1.png)

```js
import React from 'react';
import { Chart, Geom, Axis, Tooltip, Coord, Label } from 'bizcharts@3.5.8';
import numeral from 'numeral';

// CDN START

class BarLabel extends React.Component {
  render() {
    const data = [
      {
        age: '18以下',
        count: 0.08,
      },
      {
        age: '19-25',
        count: 0.12,
      },
      {
        age: '26-30',
        count: 0.15,
      },
      {
        age: '31-35',
        count: 0.25,
      },
      {
        age: '36-40',
        count: 0.2,
      },
      {
        age: '41-45',
        count: 0.15,
      },
      {
        age: '46以上',
        count: 0.05,
      },
    ];
    const cols = {};
    return (
      <div>
        <Chart height={600} width={800} data={data} scale={cols} padding={['auto', 100, 'auto']}>
          <Coord transpose />
          <Axis name="age" />
          <Axis name="count" visible={false} />
          <Tooltip />
          {/* 凸显类型 color={['age', '#E6F6C8-#3376CB']} */}
          <Geom type="interval" position="age*count" color={['count', '#E6F6C8-#3376CB']}>
            <Label content={['age*count', (name, value) => numeral(value || 0).format('0.0%')]} />{' '}
          </Geom>
        </Chart>
      </div>
    );
  }
}

// CDN END
ReactDOM.render(<BarLabel />, mountNode)

```
