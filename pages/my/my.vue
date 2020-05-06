<template>
	<view class="container">
		<view class="top-container">
			<view class="top-left">
				<text class="username">{{userInfo.name}}</text>
				<text class="department">{{userInfo.department}}-{{userInfo.position}}</text>
			</view>
			<image class="avatar" src="../../static/images/icon/my.png"></image>
		</view>
		<view class="grids-container">
			<block v-for="(grid) in gridsArr" :key="grid.id">
				<view class="grids-item" @click="navTo(grid)">
					<text class="grid-title">{{grid.title}}</text>
					<text class="grid-num"><text class="grid-num-num">{{grid.num}}</text>个</text>
				</view>
			</block>
		</view>
	</view>
</template>

<script>
	
	export default {
		data() {
			return {
				userInfo:{
					name:'张三',
					department:'机电一室',
					position:'检测员',
					qua:'监检师'
				},
				gridsArr:[
					{
						id:'waitingTest',
						title:'待检测',
						num:7,
						url:'/pages/index/index?tab=waitingTest',
						urlType:'switchTab'
					},{
						id:'msg',
						title:'消息',
						num:17,
						url:'/pages/message/message',
						urlType:'navTo'
					},
					{
						id:'lostOrder',
						title:'累计丢单',
						num:10
					},{
						id:'finished',
						title:'累计完成',
						num:10,
						url:'/pages/index/index?tab=finished',
						urlType:'switchTab'
					}
				]
			}
		},
		methods: {
			navTo(grid){
				console.log('grid',grid)
				if(grid.urlType && grid.urlType == 'switchTab'){
					uni.switchTab({
						url:grid.url
					})
				}else if(grid.urlType && grid.urlType=='navTo'){
					uni.navigateTo({
						url:grid.url
					})
				}
			}
		},
		
	}
</script>

<style>
.container{
	background-color: #f2f2f2;
	width:100vw;
	height:100vh;
}
.top-container{
	height:200rpx;
	background-color: #ffffff;
	/* border:1px solid #000000; */
	width:calc(100vw - 60 rpx);
	padding:30rpx;
}
.top-container{
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	align-items: center;
}
.top-left{
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}
.username{
	font-weight: bold;
	margin-bottom:20rpx;
	font-size:48rpx;
	
}
.department{
	font-size:26rpx;
	color:#808080;
}
.avatar{
	width:150rpx;
	height:150rpx;
	border-radius: 50%;
	border:1px solid #000000;
}
.grids-container{
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	width:100vw;
	height:calc((100vw - 70rpx)/4 - 40rpx);
	margin-top:20rpx;
}
.grids-container .grids-item{
	background-color: #ffffff;
	width:calc((100vw - 70rpx)/4 - 40rpx);
	height:100%;
	padding:20rpx;
	font-size:30rpx;
	font-weight: bold;
	
}
.grids-item{
	display: flex;
	flex-direction: column;
	justify-content: space-around;
}
.grid-num{
	color:#aaaaaa;
}
.grid-num-num{
	color: #E73822;
}
</style>
