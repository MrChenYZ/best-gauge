# 本套代码是根据个人需求所做
	本组件参考uChart的方法，根据个人需求自定义一个仪表盘
	
## 温湿度传感器

> 引入组件

```
	//引入组件文件
	import bestGauge from '../../components/best-gauge/best-gauge.vue'

	//声明组件
	export default {
		components:{
			bestGauge
		},
		data() {
			let _width = uni.upx2px(350);
			return {
				gaugeOption:{ //定义参数
					id: 'gaugeId0',
					value: 75.8,
					axisTickLength: 2//该属性与axisTick互斥，存在axisTickLength并大于0，axisTick就无效
				}
			}
		}
	}
```

> 使用组件

```
	<best-gauge :config="gaugeOption"></best-gauge>
```

> 属性说明

属性 | 类型 | 是否必填 | 默认值 | 说明
:-:|:-:|:-:|:-:|-
id | String | true | 'rgba(255,255,255,1)' | canvas的id
bgColor | String | false | 'rgba(255,255,255,1)' | canvas外层view背景颜色
startAngle | Number | false | 0.75 | 仪表盘开始角度,详细见组件备注
endAngle | Number | false | 0.25 | 仪表盘结束角度,详细见组件备注
width | Number | false | 350(upx) | 仪表盘canvas宽度，多少自定义
status | Number/Boolean | false | 0 | 离线（不需要按钮就设置为false）
padding | Number | false | 10(upx) | 仪表盘距离canvas的内边距
min | Number | false | 0 | 仪表盘最小值
max | Number | false | 100 | 仪表盘最大值
value | Number | false | 75.8 | 仪表盘当前数值
unit | String | false | '%' | 仪表盘单位
name | String | false | '图例名称' | 仪表盘名字
detail | Object | false | 看后面详情 | 仪表盘除刻度以为的数值位置、字体大小、字体粗细、字体颜色、对其方式，详见：[数值位置](#detail "数值位置")
axisTickLength | Number | false | axisTickLength跟axisTick都不填的话，默认是一个数轴 | 仪表盘刻度圈数
axisTick | Object/Array | false | 看后面详情 | 数轴刻度设置，详见：[刻度详情](#axisTick "刻度详情")

> <a id="detail">数值参数</a>

属性 | 类型 | 是否必填 | 说明
:-:|:-:|:-:|-
title | object | true | 标题数值位置、字体大小、字体粗细、颜色、对其方式
value | object | true | 数值数值位置、字体大小、字体粗细、颜色、对其方式
unit | object | true | 单位数值位置、字体大小、字体粗细、颜色、对其方式

> 数值参数详解

属性 | 类型 | 是否必填 | 默认值（title表示title下面的默认值） | 说明
:-:|:-:|:-:|:-:|-
offsetCenter | Array | false | title:[0,-40]; value:[0,40]; unit:[0,40]（单位upx） | 数值位置
color | String | false | title:'#888888'; value:'#323232'; unit:'#323232' | 字体颜色
fontSize | Number | false | title:24; value:40; unit:22（单位upx） | 字体大小
fontWeight | String | false | title:500; value:bolder; unit:500 | 字体粗细
textAlign | String | false | 'center' | 对其方式

> <a id="axisTick">刻度详情</a>

属性 | 类型 | 是否必填 | 默认值 | 说明
:-:|:-:|:-:|:-:|-
width | Number | false | 25(upx) | 大刻度宽度
number | Number | false | 10 | 轴数量（相当于几等分）
color | String | false | '#369c96,#d5d5d5' | 轴颜色(第一个值--指针之前的颜色，之后的颜色)
subNumber | Number | false | 10 | 一个大刻度分成几个小刻度
subWidth | Number | false | 25(upx) | 小刻度宽度
subHeight | Number | false | 1 | 小刻度高度
padding | Number | false | 25(upx) | 距离上一圈距离刻度距离
