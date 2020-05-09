<template>
	<view class="list">
		<!-- 一级 -->
		<scroll-view class="list-left" scroll-y :style="'height:'+height+'px'">
			<view v-if="dataList.length>0" class="nav" @click="categoryClickMain(item.groupId,index)" :key="item.groupId" :class="index==categoryActive?'active':''" v-for="(item,index) in dataList">
				<view>{{item.groupName}}</view>
			</view>
		</scroll-view>
		<!-- 二级 -->
		<scroll-view class="list-right" scroll-y :scroll-top="scrollTop" @scroll="scroll" :style="'height:'+height+'px'" scroll-with-animation>
			<view class="content">
			   <block v-for="(item,index) in rightView" :key="item.id">
					<view class="row">
						<image :src="item.src" class="row-portrait"></image>
						{{item.name}}
						<view class="row-icon" v-for="n in item.star">
							<image src="../../static/images/icon/star.png"></image>
						</view>							
						<view v-if="item.num!=0" class="row-total">{{item.num}}</view>
					</view>	   
			   </block>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			    dataList: [
					{
						groupId:1,
						groupName:"检测组一",
						subs:[
							{
								id:0,
								name:"总数",
								src:"../../static/images/icon/inspector.png",
								num:1111,
								star:4
							},
							{
								id:1,
								name:"张一",
								src:"../../static/logo.png",
								num:0,
								star:3
							},
							{
								id:2,
								name:"张一",
								src:"../../static/logo.png",
								num:0,
								star:4
							},
							{
								id:3,
								name:"张一",
								src:"../../static/logo.png",
								num:0,
								star:3
							},
							{
								id:4,
								name:"张一",
								src:"../../static/logo.png",
								num:0,
								star:4
							},
							{
								id:5,
								name:"张一",
								src:"../../static/logo.png",
								num:0,
								star:5
							},
							{
								id:6,
								name:"张一",
								src:"../../static/logo.png",
								num:0,
								star:4
							},
							{
								id:7,
								name:"张一",
								src:"../../static/logo.png",
								num:0,
								star:3
							}
						],
					},
					{
						groupId:2,
						groupName:"检测组二",
						subs:[
							{
								id:0,
								name:"总数",
								src:"../../static/images/icon/inspector.png",
								num:2222,
								star:5
							},
							{
								id:1,
								name:"张二",
								src:"../../static/logo.png",
								num:0,
								star:4
							},
							{
								id:2,
								name:"张二",
								src:"../../static/logo.png",
								num:0,
								star:3
							}
						],
					},
					{
						groupId:3,
						groupName:"检测组三",
						subs:[
							{
								id:0,
								name:"总数",
								src:"../../static/images/icon/inspector.png",
								num:3333,
								star:4
							},
							{   id:1,
								name:"张三",
								src:"../../static/logo.png",
								num:0,
								star:3
							},
							{   id:2,
								name:"张三",
								src:"../../static/logo.png",
								num:0,
								star:5
							}
						],
					},
					{
						groupId:4,
						groupName:"检测组四",
						subs:[
							{
								id:0,
								name:"总数",
								src:"../../static/images/icon/inspector.png",
								num:4444,
								star:5
							},
							{
								id:1,
								name:"张四",
								src:"../../static/logo.png",
								num:0,
								star:4
							},
							{
								id:2,
								name:"张四",
								src:"../../static/logo.png",
								num:0,
								star:5
							}
						],
					},
					{
						groupId:5,
						groupName:"检测组五",
						subs:[
							{
								id:0,
								name:"总数",
								src:"../../static/images/icon/inspector.png",
								num:5555,
								star:3
							},
							{
								id:1,
								name:"张五",
								src:"../../static/logo.png",
								num:0,
								star:4
							},
							{
								id:2,
								name:"张五",
								src:"../../static/logo.png",
								num:0,
								star:2
							}
						],
					},
					{
						groupId:6,
						groupName:"检测组六",
						subs:[
							{
								id:0,
								name:"总数",
								src:"../../static/images/icon/inspector.png",
								num:6666,
								star:4
							},
							{
								id:1,
								name:"张六",
								src:"../../static/logo.png",
								num:0,
								star:5
							},
							{
								id:2,
								name:"张六",
								src:"../../static/logo.png",
								num:0,
								star:2
							}
						],
					}	
				],
			    height: 0,
			    categoryActive: 0,
			    scrollTop: 0,
			    scrollHeight: 0,
				rightView:[],//右边内容
				groupName:'',
			    isActive: 0 ,//默认激活的选项卡,
				
			}
		},
		onLoad() {
		    this.height = uni.getSystemInfoSync().windowHeight;
			this.rightView=this.dataList[0].subs;
		},
		methods: {
			categoryClickMain(groupId,index) {
				this.categoryActive = index;
				let current = this.dataList.find(item => item.groupId === groupId);		    
				if(current) {
					//this.rightView = current.subs[0];
					this.rightView = current.subs;
					console.log("current",current);
					console.log("this.rightView",this.rightView);
					//console.log("current.subs",current.subs);
				}
			}	
		}
	}
</script>

<style>
page{
	background-color: #F2F2F2;
	font-size:28rpx;
}
.list{
	display: flex;
	flex-direction: row;
}
.list-left{
	width: 25vw;
}
.nav{
	height: 100rpx;
	line-height: 100rpx;
	padding-left: 20rpx;
}
.active{
	background-color: #FFFFFF;
	border-left: 8rpx #6495ED solid;
}
.list-right{
	width: 75vw;
}
.content{
	background-color: #FFFFFF;
}
.row{
	width: 75vw;
	height: 130rpx;	
	display: flex;
	flex-direction: row;
	align-items: center;
	padding-left: 40rpx;
	position: relative;
}
.row-portrait{
	width: 64rpx;
	height: 64rpx;
	border-radius: 50%;
	margin-right: 20rpx;
}
.row-icon{
	margin-left: 10rpx;
	margin-top: 20rpx;
}
.row-icon image{
	width: 30rpx;
	height: 30rpx;
	
}
.row-total{
	width: 120rpx;
	height: 50rpx;
	border-radius: 25rpx;
	background-color: #6495ED;
	margin-left: 40rpx;
	color: #FFFFFF;
	text-align: center;
	line-height: 50rpx;
	position: absolute;
	top:40rpx;
	right:80rpx ;
}
 

</style>
