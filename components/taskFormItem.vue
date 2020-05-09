<template>
	<view>
		<view class="container-s">
			<view class="container-s-label">{{item.label}}</view>
			<view class="container-s-value"><text v-if="! item.slot">{{item.value}}</text><slot name="formRight" /></view>
			
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:['item']
	}
</script>

<style>
.container-s{
	height:80rpx;
	line-height:80rpx;
	display: flex;
	flex-direction: row;
	justify-content: space-between;
	border-bottom:2rpx solid #eaeaea; 
	margin-top:4rpx;
	margin:0 auto;
	width:calc(100% - 20rpx)
}
.container-s-label{
	height:50rpx;
	/* background-color: #007AFF; */
	color:#000000;
	font-size:26rpx;
}
.container-s-value{
	height:50rpx;
	text-align: right;
	color:#a4a4a4;
	display: flex;
	font-size:26rpx;
	flex-direction: row;
	/* background-color: #4CD964; */
	/* font-weight:bold; */
	
}
</style>
