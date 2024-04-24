# cc-treeChartTwo

#### 使用方法 
```使用方法
<template>
	<view class="content">


		<view class="mui-content" style="margin-top: 16px;">



			<l-echart ref="chart" @finished="init"></l-echart>

		</view>


	</view>
</template>

<script>
	import LEchart from '@/uni_modules/lime-echart/components/l-echart/l-echart.vue';
	import * as echartsLime from '@/uni_modules/lime-echart/static/echarts.min'

	export default {
		components: {
			LEchart
		},
		data() {
			return {
				option: {},
			}
		},


		mounted() {

		},

		methods: {

			async init() {

				//  颜色设定 不同颜色寓意不同权重
				var fatherColor = 'green';
				var midColor = 'rgb(193, 92, 31)';
				var smallColor = 'rgb(247, 203, 174)';


				// 新能源汽车
				let swyyQ = {
					"name": "新能源汽车",
					itemStyle: {
						color: midColor
					},
					"children": [{
							"name": "大型企业",
							itemStyle: {
								color: fatherColor
							},


						},
						{
							"name": "中型企业",
							itemStyle: {
								color: midColor
							},

						},
						{
							"name": "小型企业",
							itemStyle: {
								color: smallColor
							},

						},
						{
							"name": "其他规模企业",
							itemStyle: {
								color: fatherColor
							},
						}
					]
				};

				// 新材料行业
				let xclkQ = {
					"name": "生物与新医药",
					itemStyle: {
						color: fatherColor
					},
					"children": [{
							"name": "大型企业",
							itemStyle: {
								color: fatherColor
							},


						},
						{
							"name": "中型企业",
							itemStyle: {
								color: midColor
							},

						},
						{
							"name": "小型企业",
							itemStyle: {
								color: smallColor
							},

						},
						{
							"name": "其他规模企业",
							itemStyle: {
								color: fatherColor
							},
						}
					]
				};;



				let data = {
					"name": "行业分类",
					itemStyle: {
						color: fatherColor
					},
					"children": [swyyQ, xclkQ]

				}
				// 获取网页宽度 设置树形条目实体宽高度
				let width = 360;
				let widthSize = 0.039 * width;
				if (widthSize > 36) {
					widthSize = 36;
				}
				let heightSize = widthSize;

				this.option = {
					tooltip: {
						trigger: 'item',
						triggerOn: 'mousemove'
					},
					series: [{
						type: 'tree',
						data: [data],
						left: '10%',
						right: '20%',
						top: '10%',
						bottom: '10%',
						symbol: 'circle',
						symbolSize: [widthSize, heightSize],
						orient: 'horizontal',
						expandAndCollapse: true,
						initialTreeDepth: 2,


						label: {
							position: 'top',
							rotate: 0,
							verticalAlign: 'middle',
							align: 'middle',
							fontSize: 12,

						},
						leaves: {
							label: {
								position: 'top',
								rotate: 0,
								verticalAlign: 'middle',
								align: 'middle'
							}
						},
						animationDurationUpdate: 150
					}]
				};

				// chart 图表实例不能存在data里
				const chart = await this.$refs.chart.init(echartsLime);
				chart.setOption(this.option)
			}



		}

	}
</script>


<style>
	.content {
		display: flex;
		flex-direction: column;

	}

	.mui-content {

		width: 360px;
		height: 600px;
	}
</style>

```