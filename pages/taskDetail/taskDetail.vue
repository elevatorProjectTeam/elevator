<template>
	<view class="container">
		<view class="top-container">
			<view class="title">{{type}}</view>
			<task-item :taskItem="taskItem"></task-item>
		</view>
		<task-form :taskForm="taskForm"></task-form>
		<button class="finished" type="warn" @click="finished">完成检测</button>
	</view>
</template>

<script>
	import taskItem from "@/components/taskItem.vue"; //顶部列表项组件
	import taskForm from '@/components/taskForm.vue'; //大的列表信息组件
	
	export default {
		data() {
			return {
				taskItem:{},
				id:0,
				type:'待检测',
				taskForm:[{
					id:'equitmentCondition',
					title:'设备概况',
					list:[{
						label:'所在地区',
						value:'东区'
					},{
						label:'设备种类',
						value:'电梯'
					},{
						label:'设备详情',
						value:'5台'
					},{
						label:'检验种类',
						value:'法定检验'
					},{
						label:'检验类别',
						value:'定期检验'
					},{
						label:'检验时间',
						value:'2018-06-07'
					},]
				},
				{
					id:'testingInfo',
					title:'检测信息',
					list:[{
						label:'检测员',
						value:'张三、李四',
						slot:'选择'
					},{
						label:'检测时间',
						value:'2019-08-26',
						slot:'calendar'
					}]
				},
				{
					id:'apartmentInfo',
					title:'申报单位信息',
					list:[{
						label:'订单号',
						value:'201805210003',
						slot:'复制'
					},{
						label:'单位名称',
						value:'竹园股份合作经济联合社'
					},{
						label:'联系人',
						value:'陈先生'
					},{
						label:'联系电话',
						value:'1360000000',
						slot:'打电话'
					},{
						label:'联系地址',
						value:'中山市小榄镇竹园路36号'
					},{
						label:'下单时间',
						value:'2018-05-11 12:10'
					},]
				},{
					id:'gradeInfo',
					title:'检测评分',
					list:[{
						label:'专业性',
						value:5,
						slot:'grade'
					},{
						label:'服务态度',
						value:4,
						slot:'grade'
					},{
						label:'响应时间',
						value:3,
						slot:'grade'
					}]
				}
				],
				taskArr:[
					{
						id:1,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社111',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:2,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社222',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:3,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社333',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:4,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社44',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:5,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社55',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
				]
			}
		},
		methods: {
			finished(){
				console.log('finished')
			}
		},
		created(){
			
		},
		onLoad(options){
			console.log('onload',options)
			this.id = options.id;
			this.taskItem = this.taskArr[this.id - 1];
			
			uni.getStorage({
				key:'currentTab',
				success:(res)=>{
					console.log('tabbbbbbb',res.data)
					this.type = res.data.title;
				}
			})
			
		},
		components:{
			'task-form':taskForm,
			'task-item':taskItem,
			
		}
	}
</script>

<style>
.container{
	background-color: #eaeaea;
}
.title{
	color:#ffffff;
	/* padding-left:30rpx; */
	padding:30rpx;
	font-weight:bold;
}
.top-container{
	background-color:#3291F8;
	padding-bottom:20rpx;
}
.finished{
	/* background-color: #E73822;
	color:#ffffff;	 */
	border-radius:none;
}
</style>
