# 分组柱状图（adjust）

![预览](https://z.alicdn.com/alickn/chu-ko-no/2020-5-6/bizcharts/877d1bcd-331d-4bc7-bdde-7441a51d812d/877d1bcd-331d-4bc7-bdde-7441a51d812d.png)

```js
import React from "react";
import {
  G2,
  Chart,
  Tooltip,
  Interval,
} from "bizcharts";

function Grouped() {
  return (
    <Chart height={300} padding="auto" data={data} autoFit>
      <Interval
        adjust={[
         {
            type: 'dodge',
            marginRatio: 0,
          },
        ]}
        color="name"
        position="月份*月均降雨量"
      />
      <Tooltip shared />
    </Chart>
  );
}

const data = [
  { name: 'London', 月份: 'Jan.', 月均降雨量: 18.9 },
  { name: 'London', 月份: 'Feb.', 月均降雨量: 28.8 },
  { name: 'London', 月份: 'Mar.', 月均降雨量: 39.3 },
  { name: 'London', 月份: 'Apr.', 月均降雨量: 81.4 },
  { name: 'London', 月份: 'May', 月均降雨量: 47 },
  { name: 'London', 月份: 'Jun.', 月均降雨量: 20.3 },
  { name: 'London', 月份: 'Jul.', 月均降雨量: 24 },
  { name: 'London', 月份: 'Aug.', 月均降雨量: 35.6 },
  { name: 'Berlin', 月份: 'Jan.', 月均降雨量: 12.4 },
  { name: 'Berlin', 月份: 'Feb.', 月均降雨量: 23.2 },
  { name: 'Berlin', 月份: 'Mar.', 月均降雨量: 34.5 },
  { name: 'Berlin', 月份: 'Apr.', 月均降雨量: 99.7 },
  { name: 'Berlin', 月份: 'May', 月均降雨量: 52.6 },
  { name: 'Berlin', 月份: 'Jun.', 月均降雨量: 35.5 },
  { name: 'Berlin', 月份: 'Jul.', 月均降雨量: 37.4 },
  { name: 'Berlin', 月份: 'Aug.', 月均降雨量: 42.4 },
];



ReactDOM.render(<Grouped />, mountNode)

```
