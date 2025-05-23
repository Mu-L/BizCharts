# BizCharts散点图

![预览](http://bizcharts-resource.oss-cn-zhangjiakou.aliyuncs.com/images/77c7b250-9979-11ea-9761-adf4e02ffa04.png)

```js
import $ from "jquery";
import React from "react";
import {
  G2,
  Chart,
  Geom,
  Axis,
  Tooltip,
  Coord,
  Label,
  Legend,
  View,
  Guide,
  Shape,
  Facet,
  Util
} from "bizcharts@3.5.8";

let data;
$.ajax({
  url: "https://alifd.alibabausercontent.com/materials/@bizcharts/point-scatter/0.2.8/mock.json",
  async : false,
  success: (iData) => { data = iData }
});

class Scatter extends React.Component {
  render() {
    return (
      <div>
        <Chart height={window.innerHeight} data={data} forceFit>
          <Tooltip
            showTitle={false}
            crosshairs={{
              type: "cross"
            }}
            itemTpl="<li data-index={index} style=&quot;margin-bottom:4px;&quot;><span style=&quot;background-color:{color};&quot; class=&quot;g2-tooltip-marker&quot;></span>{name}<br/>{value}</li>"
          />
          <Axis name="height" />
          <Axis name="weight" />
          <Geom
            type="point"
            position="height*weight"
            opacity={0.65}
            shape="circle"
            size={4}
            tooltip={[
              "gender*height*weight",
              (gender, height, weight) => {
                return {
                  name: gender,
                  value: height + "(cm), " + weight + "(kg)"
                };
              }
            ]}
          />
        </Chart>
      </div>
    );
  }
}

ReactDOM.render(<Scatter />, mountNode)

```
