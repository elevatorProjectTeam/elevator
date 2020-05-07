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
@font-face {font-family: "iconfont";
  src: url('~@/static/iconfont-my/iconfont.ttf'); /* IE9 */
  src: url('~@/static/iconfont-my/iconfont.eot') format('embedded-opentype'), /* IE6-IE8 */
  url('data:application/x-font-woff2;charset=utf-8;base64,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') format('woff2'),
  url('~@/static/iconfont-my/iconfont.woff') format('woff'),
  url('~@/static/iconfont-my/iconfont.ttf') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
  url('~@/static/iconfont-my/iconfont.svg') format('svg'); /* iOS 4.1- */
}

.iconfont {
  font-family: "iconfont" !important;
  font-size: 36rpx;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: inline-block;
  color:#65B7E7;
}

.icon-jiantou:before {
  content: "\e621";
  color: #A6A4A4;
}

.icon-huangguan:before {
  content: "\e620";
}

.icon-liwu:before {
  content: "\e60a";
}

.icon-shoucang:before {
  content: "\e613";
}

.icon-gongwenbao:before {
  content: "\e70b";
}

.icon-rili:before {
  content: "\e64f";
  color: #DF0902;
}

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
