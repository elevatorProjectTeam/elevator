<template>
	<view class="container">
		<view class="top-container">
			<view class="top-left">
				<text class="username">{{userInfo.name}}</text>
				<text class="department">{{userInfo.department}}-{{userInfo.position}}</text>
				<view class="authorize">
					<text v-if="authorize" class="iconfont icon-rili"></text>
					<text>{{authorize?'已认证':'未认证'}}</text>
				</view>
			</view>
			<view>
				<image class="avatar" src="../../static/images/icon/my.png"></image>
				<view class="iconfont icon-huangguan huangguan"></view>
			</view>
		</view>
		<view class="grids-container">
			<block v-for="(grid) in gridsArr" :key="grid.id">
				<view class="grids-item" @click="navTo(grid)">
					<text class="grid-title">{{grid.title}}</text>
					<text class="grid-num"><text class="grid-num-num">{{grid.num}}</text>个</text>
				</view>
			</block>
		</view>
		<view class="menu-container">
			<block v-for="(menu,index) in menuArr" :key="index">
				<view class="menu-item" @click="navTo(menu)">
					<text class="iconfont" :class="menu.icon"></text>
					<view class="menu-title">{{menu.title}}</view>
					<view class="menu-info">{{menu.info}}</view>
					<text class="iconfont icon-jiantou"></text>
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
						url:'/pages/index/index',
						urlType:'switchTab',
						button:''
					},{
						id:'msg',
						title:'消息',
						num:17,
						url:'/pages/message/message',
						urlType:'navTo'
					},
					{
						id:'difficultList',
						title:'疑难单',
						num:10,
						url:'/pages/index/index',
						urlType:'switchTab',
						button:"去分配"
					},{
						id:'finished',
						title:'累计完成',
						num:10,
						url:'/pages/index/index',
						urlType:'switchTab',
						button:''
					}
				],
				menuArr:[
					{
						title:'个人详情',
						icon:'icon-shoucang',
						url:'/pages/userInfo/userInfo',
						urlType:'navTo'
					},
					{
						title:'绑定手机',
						icon:'icon-liwu',
						info:'133********'
					},
					{
						title:'关于我们',
						icon:'icon-gongwenbao'
					}
				],
				authorize:true
			}
		},
		methods: {
			navTo(grid){
				console.log('grid',grid)
				if(grid.urlType && grid.urlType == 'switchTab'){
					uni.switchTab({
						url:grid.url
					});
					uni.setStorage({
						key:'currentTab',
						data:{
							id:grid.id,
							title:grid.title,
							button:grid.button
						}
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
.authorize{
	margin-top: 10rpx;
	width: 150rpx;
	height: 45rpx;
	text-align: center;
	font-size: 26rpx;
	border: solid 3rpx #bbbbbb;
	border-radius: 25rpx;
	color:#808080;
}
.avatar{
	width:150rpx;
	height:150rpx;
	border-radius: 50%;
	border:1px solid #000000;
}
.huangguan{
	background-color: #FDDE9D;
	color: #CAAA60;
	width: 40rpx;
	height: 40rpx;
	border-radius: 50%;
	text-align: center;
	font-size: 20rpx;
	font-weight: bold;
	line-height: 40rpx;
	position: relative;
	left: -45rpx;
	top:-10rpx;
}
.grids-container{
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	width:100vw;
	/*height:calc((100vw - 70rpx)/4 - 40rpx);*/
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
.menu-container{
	margin-top: 20rpx;
	width: 100vw;
}
.menu-item{
	height: 80rpx;
	width: calc(100vw-40rpx);
	line-height: 80rpx;
	padding-left: 20rpx;
	padding-right: 20rpx;
	font-size: 30rpx;
	background-color: #FFFFFF;
	margin-bottom: 5rpx;
	display: flex;
	justify-content: space-around;
	color: #5B5B5B;
}
.menu-title{
	flex-grow: 1;
	margin-left: 10rpx;
}
</style>
