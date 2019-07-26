<template>
	<view class="content">
		<view class="title">温湿度传感器</view>
		<view class="flex echart-box">
			<view class="flex-1">
				<best-gauge :config="gaugeOption0"></best-gauge>
			</view>
			<view class="flex-1">
				<best-gauge :config="gaugeOption1"></best-gauge>
			</view>
		</view>
		<view class="text" @click="update">更新数据</view>
		<image class="logo" src="/static/logo.png"></image>
	</view>
</template>

<script>
	import bestGauge from '../../components/best-gauge/best-gauge.vue'
	export default {
		data() {
			let _width = uni.upx2px(350);
			return {
				gaugeOption0:{
					id: 'gaugeId0',
					value: 75.8,
					axisTickLength: 2//该属性与axisTick互斥，存在axisTickLength并大于0，axisTick就无效
				},
				gaugeOption1: {
					id: 'gaugeId1',
					bgColor:'rgba(255,255,255,1)',
					startAngle: 0.75,
					endAngle: 0.25,
					width: _width,
					status: 1,//设备是否在线 0 离线 1在线
					padding: 10,
					min: 0,
					max: 100,	
					value: 75.8,
					unit: '%',
					name: '当前湿度',
					detail: {//数值单位设置
						title: {//name字体位置设置
							color:'#888888',
							fontSize: uni.upx2px(24),
							fontWeight:'500',
							offsetCenter:[0,uni.upx2px(-40)],
							textAlign:'center'
						},
						value: {
							color:'#323232',
							fontSize: uni.upx2px(48),
							fontWeight:'bolder',
							offsetCenter:[0,uni.upx2px(40)],//距离圆心直径偏移
							textAlign:'center'
						},
						unit: {
							color:'#323232',
							fontSize: uni.upx2px(22),
							fontWeight:'bolder',
							offsetCenter:[0,uni.upx2px(40)],//距离圆心直径偏移
							textAlign:'center'
						}
					},
					axisTick:[//轴刻度线
						{
							width: uni.upx2px(25),//轴长
							number: 6,//轴数量（相当于几等分）
							color: '#369c96,#d5d5d5',//轴颜色(第一个值--指针之前的颜色，之后的颜色)
							subNumber: 10,//一个大刻度分成几个小刻度
							subHeight:1,
							subWidth:  uni.upx2px(25),
							padding: uni.upx2px(10)//刻度距离边距
						},
						{
							width: uni.upx2px(10),//轴长
							number: 6,//轴数量（相当于几等分）
							color: '#d5d5d5',//轴颜色(第一个值--指针之前的颜色，之后的颜色)
							subNumber: 10,//一个大刻度分成几个小刻度
							subHeight:1,
							subWidth:  uni.upx2px(6),
							padding: uni.upx2px(25)//刻度距离边距
						}
					]
				}
			}
		},
		components: {
			bestGauge
		},
		onLoad() {

		},
		methods: {
			update:function(){
				let gaugeOption0 = JSON.parse(JSON.stringify(this.gaugeOption0))
				let gaugeOption1 = JSON.parse(JSON.stringify(this.gaugeOption1))
				gaugeOption0.value = this.getRandom(gaugeOption0.max);
				gaugeOption1.value = this.getRandom(gaugeOption1.max);
				this.gaugeOption0 = gaugeOption0;
				this.gaugeOption1 = gaugeOption1;
			},
			getRandom:function(max){
				max = max || 100;
				let _random = (Math.random() * max).toFixed(1);
				return _random * 1;
			}
		}
	}
</script>

<style>
	.content {
		width: 100%;
		/* #ifdef H5 */
		min-height: calc(100vh - var(--window-bottom) - var(--window-top));
		/* #endif */
		/* #ifndef H5 */
		min-height: 100vh;
		/* #endif */
		background-color: #fff;
	}
	.title{
		font-size: 30upx;
		text-align: center;
		padding: 100upx 40upx;
	}
	
	.flex{display: -webkit-box;display: -ms-flexbox;display: flex;}
	.flex-1{position: relative;-webkit-box-flex:  1;-ms-flex:  1;flex:  1;width: 50%;}
	
	.logo {
		height: 400upx;
		width: 400upx;
		display: block;
		margin: 0 auto;
	}

	.text {
		text-align: center;
		width: 240upx;
		line-height: 70upx;
		display: block;
		margin: 50upx auto;
		border: 1px solid #369c96;
		font-size: 28upx;
		border-radius: 10upx;
		color: #369c96;
	}
</style>
