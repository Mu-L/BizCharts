# 气泡图-自定义 shape

![预览](http://bizcharts-resource.oss-cn-zhangjiakou.aliyuncs.com/images/77b16b30-9979-11ea-8225-e30c1937e15c.png)

```js
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

class Bubbleimage extends React.Component {
  render() {
    // 自定义 shape, 支持图片形式的气泡
    Shape.registerShape("point", "image", {
      drawShape: function(cfg, container) {
        cfg.points = this.parsePoints(cfg.points);
        const coord = this._coord;
        container.addShape("line", {
          attrs: {
            x1: cfg.points[0].x,
            y1: cfg.points[0].y,
            x2: cfg.points[0].x,
            y2: coord.start.y,
            stroke: "#ccc",
            lineWidth: 1,
            lineDash: [4, 2]
          }
        });
        return container.addShape("image", {
          attrs: {
            x: cfg.points[0].x - (12 * cfg.size) / 2,
            y: cfg.points[0].y - 12 * cfg.size,
            width: 12 * cfg.size,
            height: 12 * cfg.size,
            img: cfg.shape[1]
          }
        });
      }
    });
    const data = [
      {
        name: "Internet Explorer",
        value: 26
      },
      {
        name: "Chrome",
        value: 40
      },
      {
        name: "Firefox",
        value: 30
      },
      {
        name: "Safari",
        value: 24
      },
      {
        name: "Opera",
        value: 15
      },
      {
        name: "Undetectable",
        value: 8
      }
    ];
    const imageMap = {
      "Internet Explorer":
        "https://gw.alipayobjects.com/zos/rmsportal/eOYRaLPOmkieVvjyjTzM.png",
      Chrome:
        "https://gw.alipayobjects.com/zos/rmsportal/dWJWRLWfpOEbwCyxmZwu.png",
      Firefox:
        "https://gw.alipayobjects.com/zos/rmsportal/ZEPeDluKmAoTioCABBTc.png",
      Safari:
        "https://gw.alipayobjects.com/zos/rmsportal/eZYhlLzqWLAYwOHQAXmc.png",
      Opera:
        "https://gw.alipayobjects.com/zos/rmsportal/vXiGOWCGZNKuVVpVYQAw.png",
      Undetectable:
        "https://gw.alipayobjects.com/zos/rmsportal/NjApYXminrnhBgOXyuaK.png"
    };
    const cols = {
      value: {
        nice: false,
        max: 60,
        min: 0
      }
    };
    return (
      <div>
        <Chart
          data={data}
          padding={[20, 20, 90]}
          scale={cols}
          forceFit
        >
          <Axis name="name" />
          <Axis name="value" visible={false} />
          <Tooltip />
          <Geom
            type="point"
            position="name*value"
            color="name"
            shape={[
              "name",
              name => {
                return ["image", imageMap[name]]; // 根据具体的字段指定 shape
              }
            ]}
            size="value"
            style={{
              stroke: "#fff",
              lineWidth: 1,
              fillOpacity: 1
            }}
          >
            <Label
              content="value"
              offset={-20}
              textStyle={{
                fontSize: 16 // 文本大小
              }}
            />
          </Geom>
        </Chart>
      </div>
    );
  }
}

ReactDOM.render(<Bubbleimage />, mountNode)

```
