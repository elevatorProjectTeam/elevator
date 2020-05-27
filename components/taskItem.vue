<template>
	<view class="padding-container" @click="toDetails(taskItem.id)">
		<view class="container">
			<image :src="taskItem.src" class="img" mode="aspectFit"></image>
			<view class="r-content">
				<view>
					<text>镇区：</text>
					<block v-for="(townShip,index) in taskItem.townShips" :key="index">
						<text style="margin-left:20rpx;">{{townShip}}</text>
					</block>
				</view>
				<view>检测数量：<view class="e-num">{{taskItem.eNum}}台</view></view>
				<view>检测人员：<view class="e-num">{{taskItem.inspectorNumber}}人</view></view>
				<view class="time">{{taskItem.time}}</view>
				<view class="tags">
					<block v-for="(tag,index) in taskItem.tags" :key="tag">
						<view class="tag-item">{{tag}}</view>
					</block>
				</view>
			</view>
		</view>
		<slot name="button" />
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
				// taskItem:{
				//  src:"~@/static/images/temp/temp01.png",
				// 	orgName:'竹源股份合作经济联合社',
				// 	eNum:5,
				// 	address:'中山市小榄镇竹源路36号',
				// 	time:'2019-08-16',
				// 	tags:['电梯','法定检验','年度检验']
				// }
			};
		},
		props:['taskItem','currentTab'],
		methods:{
			toDetails(id){
				var thisTask = this.taskItem;
				uni.navigateTo({
					url:'/pages/taskDetail/taskDetail?taskItem='+ encodeURIComponent(JSON.stringify(thisTask)),
					
					success:(res)=>{
						console.log(res)
						uni.setStorage({
							key:'currentTab',
							data:this.currentTab
						})
					}
				})
				
				
				/* uni.navigateTo({
					url:'/pages/taskDetail/taskDetail?id='+id,
					success(res){
						// console.log(res)
					}
				}) */
			}
		},
		created(){
			// uni.getStorage({
			// 	key:'currentTab',
			// 	success:res=>{
			// 		this.currentTab = res.data
			// 		console.log('taskItem onload',this.currentTab)
			// 	}
			// })
		}
	}
</script>

<style>


.button-container{
	height:70rpx;
}
.e-button{
	color:#3291F8 !important;
	border-color:#3291F8 !important;
	display: inline-block;
	float: right;
}
.padding-container{
	margin:0 auto;
	padding:20rpx 30rpx;
	display: block;
	width:calc(95vw - 60rpx);
	clear: both;
	border-bottom: 10rpx solid #f2f2f2;
	background-color: #ffffff;
}
.container{
	display: flex;
	flex-direction: row;
	background-color: #ffffff;
	width:calc(100vw-60rpx);
	
}
.img{
	width:150rpx;
	height:280rpx;
}
.r-content{
	flex:1;
	font-size:24rpx;
	display: flex;
	flex-direction: column;
	justify-content: space-around;
	padding:30rpx 0 30rpx 30rpx;
}
.r-content .organization-name{
	font-size:34rpx;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}
.r-content .organization-name .name{
	flex:1;
}
.e-num{
	/* text-align: right; */
	display: inline-block;
	color:#FA783C;
}
.r-content .address{
	font-size:28rpx;
}
.r-content .time{
	color:#333333;
}
.tags{
	display: flex;
	flex-direction: row;
	justify-content: space-between;
}
.tags .tag-item{
	padding:10rpx 25rpx;
	background-color: #FEF4E9;
	color:#E29F5C;
}
.r-content .time{
	
}
</style>
