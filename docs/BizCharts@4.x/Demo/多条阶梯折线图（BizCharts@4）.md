# 多条阶梯折线图（BizCharts@4）

![预览](http://bizcharts-resource.oss-cn-zhangjiakou.aliyuncs.com/images/ee8b9d10-3b7d-11eb-9199-e520dbc463c0.png)

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
} from "bizcharts";
import DataSet from "@antv/data-set";

class Stepseries extends React.Component {
	render() {
		const data = [
			{
				month: "Jan",
				series2: 51,
				series1: 125
			},
			{
				month: "Feb",
				series2: 91,
				series1: 132
			},
			{
				month: "Mar",
				series2: 34,
				series1: 141
			},
			{
				month: "Apr",
				series2: 47,
				series1: 158
			},
			{
				month: "May",
				series2: 63,
				series1: 133
			},
			{
				month: "June",
				series2: 58,
				series1: 143
			},
			{
				month: "July",
				series2: 56,
				series1: 176
			},
			{
				month: "Aug",
				series2: 77,
				series1: 194
			},
			{
				month: "Sep",
				series2: 99,
				series1: 115
			},
			{
				month: "Oct",
				series2: 106,
				series1: 134
			},
			{
				month: "Nov",
				series2: 88,
				series1: 110
			},
			{
				month: "Dec",
				series2: 56,
				series1: 91
			}
		];
		const ds = new DataSet();
		const dv = ds.createView().source(data);
		dv.transform({
			type: "fold",
			fields: ["series1", "series2"],
			key: "key",
			value: "value"
		});
		const cols = {
			month: {
				range: [0, 1]
			}
		};
		return (
			<Chart height={400} appendPadding={[10,0,0,0]} data={dv} scale={cols} autoFit>
				<Legend />
				<Axis name="month" />
				<Axis name="value" />
				<Tooltip
					crosshairs={{
						type: "y"
					}}
				/>
				<Geom
					type="line"
					position="month*value"
					size={2}
					color={"key"}
					shape={"hv"}
				/>
			</Chart>
		);
	}
}

ReactDOM.render(<Stepseries />, mountNode)

```
