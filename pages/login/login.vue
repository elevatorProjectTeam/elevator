<template>
	<view class="content">
		<view class="title">智能派单系统</view>
		<view class="logo">
			<image src="../../static/logo.png" mode="widthFix"></image>
			<view>中山特检</view>
		</view>
		<button v-if="!getUserInfo&&canIUse" open-type="getUserInfo" @getuserinfo="wxgetUserInfo">授权登录</button>
		<view v-else-if="!canIUse" class="tip">请升级版本！</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				getUserInfo:false,
				canIUse:uni.canIUse('button.open-type.getUserInfo')
			}
		},
		onLoad(){
			this.wxgetUserInfo()
		},
		methods: {
			wxgetUserInfo(){
				var that=this;
				uni.showLoading({
					title:'加载中...'
				})
				uni.getUserInfo({
					success:res=>{
						console.log("userinfo",res)
						that.getUserInfo=true
						//登录处理，向后台传递code...
						uni.login({
							success:code=>{
								console.log("got the code")
								uni.switchTab({
									url:'/pages/index/index'
								})
								uni.hideLoading()
							}
						})
					},
					fail:() => {
						uni.showToast({
						  title: "请点击授权进行登录！",
						  icon:"none"
						})
					}
				})
			}
		}
	}
</script>

<style>
.content{
	display: flex;
	justify-content: center;
	flex-wrap: wrap;
}
.title{
	color: #F8F8F8;
	width: 100%;
	margin-top: 20rpx;
	text-align: center;
	font-size: 34rpx;
}
.logo{
	color: #3291F8;
	font-size: 34rpx;
	width: 100%;
	text-align: center;
	margin-top: 140rpx;
}
.logo image{
	margin-bottom: 30rpx;
	width: 170rpx;
	border-radius: 100rpx;
}
button{
	width: 550rpx;
	height: 80rpx;
	line-height: 80rpx;
	color: #FFFFFF;
	border-radius: 100rpx;
	background-color: #3291F8;
	margin-top: 400rpx;
}
.tip{
	text-align: center;
	font-size: 34rpx;
	width: 100%;
	margin-top: 400rpx;
}
</style>
