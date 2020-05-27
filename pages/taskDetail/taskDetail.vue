<template>
	<view class="taskD-container">
		<view class="top-container">
			<view class="title">
			{{type}} 
			<uni-icons type="arrowright" size="24" class="arrow-right" color="#ffffff"></uni-icons>			
			</view>
			
			<task-item :taskItem="taskItem"></task-item>
		</view>
		<task-form :taskForm="taskForm"></task-form>
		
		<view class="map">
			<map  id="thisMap"
			style="width: 100%; height: 300px;" 
			:latitude="map.latitude" 
			:longitude="map.longitude" 
			:markers="map.covers"
			:polyline="map.polyline"
			:include-points="map.polyline[0].points"
			enable-3D
			show-compass
			enable-overlooking
		
			
			enable-traffic
			show-location
			@tap="openMap">
			</map>
		</view>
		
		<view class="eq-container">
			<e-table></e-table>
		</view>
		<!-- <button class="finished" type="warn" @click="finished">完成检测</button> -->
	</view>
</template>

<script>
	import taskItem from "@/components/taskItem.vue"; //顶部列表项组件
	import taskForm from '@/components/taskForm.vue'; //大的列表信息组件
	import uniIcons from '@/components/uni-icons/uni-icons.vue'
	import eTable from '@/components/equipTable.vue'
	
	export default {
		data() {
			return {
				map:{
				
					latitude:23.106401,
					longitude: 113.324577 ,
					polyline:[
						{
							points:
							[
								
								{latitude:23.106401,longitude:113.324577},
								{latitude:23.126777,longitude:113.285164},
								{latitude:23.118742,longitude:113.270367},
								
							],
							color:"#0000aa",
							width:5,
						
							
						}
						
					],
					covers: [{
					    latitude:23.106401,
					    longitude:  113.324577,
					    iconPath: require('@/static/images/icon/location.png'),
						width:40,
						height:40,
						label:{
							content:'我是第一个地点',
							color:'#606060',
							fontSize:8,
							borderWidth:2,
							borderColor:'#3291F8',
							borderRadius:5,
							bgColor:'#ffffff',
							padding:10,
							textAlign:'left',
							
						},
						
					},
					{
					    latitude:23.126777,
					    longitude:  113.285164,
					    iconPath: require('@/static/images/icon/location.png'),
						width:40,
						height:40,
						label:{
							content:'我是第二个地点',
							color:'#606060',
							fontSize:8,
							borderWidth:2,
							borderColor:'#3291F8',
							borderRadius:5,
							bgColor:'#ffffff',
							padding:10,
							textAlign:'left',
							x:-0.001,
							y:-0.001
						}
					},
					{
					    latitude:23.118742,
					    longitude:  113.270367,
					    iconPath: require('@/static/images/icon/location.png'),
						width:40,
						height:40,
						label:{
							content:'我是第三个地点',
							color:'#606060',
							fontSize:8,
							borderWidth:2,
							borderColor:'#3291F8',
							borderRadius:5,
							bgColor:'#ffffff',
							padding:10,
							textAlign:'left',
							x:-0.001,
							y:-0.001
						}
					},],
					
				},
				taskItem:{},
				id:0,
				type:'待检测',
				taskForm:[
				 {
					id:'testingInfo',
					title:'检测信息',
					list:[{
						label:'检测员',
						value:'张三、李四',
						// slot:'选择'
					},{
						label:'检测时间',
						value:'2019-08-26',
						// slot:'calendar'
					}]
				}
				],
				taskArr:[
					
				]
			}
		},
		methods: {
			finished(){
				console.log('finished')
			},
			 openMap() {//点击地图
			
			      /* uni.openLocation({
			
			      latitude: this.map.latitude,
			
			      longitude: this.map.longitude,
			
			      name:"广州市广州塔",
			
			      address: "广州市广州塔"
			
			    }) */
				// debugger
				
				// debugger
			
			  },
			  //定位方法;获取当前的经纬度，也可以通过经纬度来获取当前的地理位置，比如：xx省、xx市、xx镇
			  getlocal: function() {
			  	let _this = this;
			  	//显示当前位置
			  	var map = uni.createMapContext('maps',this).$getAppMap();
			  	map.showUserLocation(true);
			  	//获取当前定位
			  	uni.getLocation({
			  		type: 'wgs84',
			  		success: function(res) {
			  			console.log('当前位置的经度：' + res.longitude);
			  			console.log('当前位置的纬度：' + res.latitude);
			  			_this.map.longitude = res.longitude;
			  			_this.map.latitude = res.latitude;
			  		}
			  	})
			  }
			  			 			
		},
		
		onReady(){
			console.log('onReady')
			let _this = this;
			let myMap = uni.createMapContext('thisMap',_this);
			console.log('map1',myMap)
			let myMap2= myMap.$getAppMap();
			console.log('map2',myMap2)
			/* setTimeout(()=>{
				let myMap2= myMap.$getAppMap();
				console.log('map2',myMap2)
			},10000) */
			
		},
		onLoad(options){
			console.log('onload1111111',options)
			
			this.taskItem = JSON.parse(decodeURIComponent(options.taskItem)) ;
			
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
			uniIcons,
			eTable
		}
	}
</script>

<style>
.taskD-container{
	background-color: #f8f8f8;
}
.taskD-container .title{
	color:#ffffff;
	/* padding-left:30rpx; */
	padding:30rpx;
	font-weight:bold;
}
.taskD-container .arrow-right{
	margin-left:30rpx;
}
.taskD-container .top-container{
	background-color:#3291F8;
	padding-bottom:20rpx;
}
.taskD-container .finished{
	/* background-color: #E73822;
	color:#ffffff;	 */
	border-radius:none;
}
</style>
