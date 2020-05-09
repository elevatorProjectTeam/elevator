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
				uni.navigateTo({
					url:'/pages/taskDetail/taskDetail?id='+id,
					success(res){
						// console.log(res)
					}
				})
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
@font-face {font-family: "iconfont";
  src: url('~@/static/iconfont/iconfont.ttf'); /* IE9 */
  src: url('~@/static/iconfont/iconfont.eot') format('embedded-opentype'), /* IE6-IE8 */
  url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAAPgAAsAAAAACAAAAAORAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHEIGVgCDHAqDRIMfATYCJAMQCwoABCAFhG0HPhsHBxHVm8vI/lBAx11bAappR7RjcSK8b2kwtVY/Vso5CB7wveqlycx2sKKOZA+yvpjmkRoNEBCdvf8W7fNViMrWnAM2KkIV3Sxr9A95KKWXpqPC2a4IvwD4n2PGqxDIDzSXrKTR3gBH0TqgyusmuwPEUwmvSwc9Bvt2CMBKkASiVJlKtdBR6JsEIDq1b9scPaFFVRQKdATmgpMKMRUTujZOuwhM8f5efCAtHTRMEv1O1dqUbkWx11Ipafw3aCQNjOHMgHgWSCABKBDtCq0tkEE0gcT6ma/IAjo6Ggw1YVbq/3/ib0WqG1K6/uNpIMzo+XYAMuCX8NriRjIz1AjISiEPDeCByHXkjAAuopMDlGooNLvdxxGPDbO3PXMnfPntMidvhiy7Vf/26zp37tS9dav2zZcDG8z28jIf4TR7pUe9mZ71Z63ydp61xrvhnHr2Orba8yJtE2KmurY6JU+uZa0zO8ra0LF+Hev4tcY6m23ChmHr+3vdvl3n5s1aHlbvocTeCZkYUmxkxZ6e2nNABRtslN6+/bOSJTXNwoeE4N3cZqcdLebs0Md5iZx27Nh0+3Pk8WPaTkv0PmQvNjefum7rv3raNSn3CktnFOFZ0NWuhf7j43X7mP6uZWbF5dWeWSufUaFlrwopm3Oq7s+uejikX8LOf2bVjitftQlr4+rMooDh4L3qz3VzgwVWcEmHfIvr1G0vR5fFS5SMrzimmhy5e98ISSxikaha0lUyvkTx4ktte+k61RK842QbOW+BbKM6LB7VTBgsx6U6yDaZ+XQD4P8RWUUW9aiH5XBZIm7I39J4p6uIP5ObOhf80m3X1Hb/wDWXav4bCmnAi+E15r1BXsMG9RXoOqU0ocX92RSFsTQ0wGoY4L0lwc3jIeSejfNBoOMZgYYDgSDRiUAoTAKYsJEBZnSKgpV4Zc+24a4HEqEsQJxRDAQutoCGE0dA4uISQmEegQkvn8CMSxKs1BHul7QRFR13B0YlaEH/IBrqnGmQnV94Qz82iuMCj/JCHmIA8iRLJy7YIQ+xZ3j7QsSBY2rhzO6GTUPQM1VoJAki/T5NXdEPJYbayW5yYFSCFvQPoqHOOa1ll/n9G/qxUVxR98P8Qh7i9JAnWQPERdo1qruUtwxvX4g4cEwtnJkZGyNK0Bcvq9BIEjqE+31KzVxTaTK9vL3DfYB1oj9PTTUhhRImljb+Q1wydp9x8SGLkwkAAAA=') format('woff2'),
  url('~@/static/iconfont/iconfont.woff') format('woff'),
  url('~@/static/iconfont/iconfont.ttf') format('truetype'), /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
  url('~@/static/iconfont/iconfont.svg') format('svg'); /* iOS 4.1- */
}

.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: inline-block;
}

.icon-dizhi:before {
  content: "\e606";
}

.icon-renwu:before {
  content: "\e644";
}

.icon-wode:before {
  content: "\e603";
}

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
