<template>
	<view class="content">
		<!-- 顶部tab -->
		
		<view class="index-tab">
			<block v-for="(tab,index) in userTab" :key="tab.id">
				<view v-bind:class="[currentTab.id == tab.id ? 'active' : '', 'tabitem',[searchFlag ? 'search-tab':'']]" @click="changeTab(tab)">{{tab.title}}</view>
			</block>
			<uni-search-bar
			v-bind:class="[searchFlag ? 'search-bar2':'','search-bar']" 
			@confirm="search" 
			@input="input"
			radius="40"
			@cancel="cancel"
			cancelButton="always"
			></uni-search-bar>
			<uni-icons v-bind:class="[searchFlag ? 'search-bar':'','search']" type="search" color="#ffffff"   size="28" style="" @click="clickSearch"></uni-icons>
			
		</view>
		<!-- 列表 -->
		<block v-for="(tab,index) in userTab" :key="tab.id">
			<block v-if="currentTab.id == tab.id" v-for="(taskItem,index2) in taskArr" :key="taskItem.id">
				<task-item :taskItem="taskItem" :currentTab="currentTab">
					<block slot="button">
						<view  class="button-container"  v-if="currentTab.button" style="z-index:999">
							<button size="mini" class="e-button" plain="true" @click.stop="toDetail(index2)" v-if="currentTab.button">{{currentTab.button}}</button>
						</view>
					</block>
					
				</task-item>
			</block>
		</block>
		<view class="no-more-task" v-if="noMoreTask">-----------没有更多数据-----------</view>
	</view>
</template>

<script>
	
	import taskItem from '@/components/taskItem.vue' 
	import uniIcons from '@/components/uni-icons/uni-icons.vue'
	import uniSearchBar from '@/components/uni-search-bar/uni-search-bar.vue'

	//列表项组件
	export default {
		data() {
			return {
				searchFlag:false,
				noMoreTask:true,
				taskPageIndex:1,
				tabLimits:[
					{
						type:'member',
						list:['waitingTest','finished']
					},
					{
						type:'manager',
						list:['difficultList','waitingTest','finished']
					}
				],	
				userType:'manager',
				tabList:[],
				userTab:[],
				currentTab:{},
				tabArr:[
					{
						id:'waitingTest',
						title:'待检测',
						button:''
					},{
						id:'finished',
						title:'已完成',
						button:''
					},{
						id:'difficultList',
						title:'疑难单',
						button:'去分配'
					}
				],
				
				taskArr:[],
			/*
			{
					id:1,
					src:"/static/images/temp/temp1.png",
					orgName:'竹源股份合作经济联合社1-待检测',
					eNum:7,
					inspectorNumber:3,
					address:'中山市小榄镇竹源路36号',
					time:'2019-08-16',
					townShips:['小榄镇','东升镇','南头镇'],
					tags:['起重机','法定检验','年度检验']
				},
				
			*/
				
			
			}
		},
		onLoad(option) {
			for(var i=0;i<this.tabLimits.length;i++){
				var thisL = this.tabLimits[i]
				if(thisL.type == this.userType){
					this.tabList = this.tabLimits[i].list;
				}
			}
			console.log('this.tabList',this.tabList)
			
			for(var i=0 ; i< this.tabList.length; i++){
				var tabListItem = this.tabList[i];
				for(var j=0 ; j < this.tabArr.length; j++){
					var tabArrItem = this.tabArr[j];
					if(tabListItem == tabArrItem.id){
						this.userTab.push(tabArrItem)
					}
				}
			}
			//获取数据
			this.taskArr = this.getTaskItem();
		},
		onShow(){
			uni.getStorage({
				key:'currentTab',
				success:(res)=>{
					console.log('success',res)
					this.currentTab = res.data;
					
				}
			})
			
		},
		methods: {
			toDetail(index){
				
				var thisTask = this.taskArr[index];
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
			},
			changeTab(tab){
				this.currentTab = tab;
				uni.setStorage({
					key:'currentTab',
					data:this.currentTab
				})
				this.taskArr = [];
				this.noMoreTask = false;
				this.taskPageIndex  = 1;
				this.taskArr = this.getTaskItem();
				console.log('changeTab',tab,this.currentTab)
			},
			clickSearch(){
				console.log('aaa')
				this.searchFlag = true;
			},
			search(){
				
			},
			input(){
				
			},
			cancel(){
				this.searchFlag = false;
			},
			getTaskItem(callBack){
				//模拟获取数据
				 var tempTaskArr = [
					{
						id:Math.round(Math.random()*1000),
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社1-待检测',
						eNum:7,
						inspectorNumber:3,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						townShips:['小榄镇','东升镇','南头镇'],
						tags:['起重机','法定检验','年度检验']
					},
					{
						id:Math.round(Math.random()*1000),
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社1-待检测',
						eNum:7,
						inspectorNumber:3,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						townShips:['小榄镇','东升镇','南头镇'],
						tags:['起重机','法定检验','年度检验']
					},
					{
						id:Math.round(Math.random()*1000),
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社1-待检测',
						eNum:7,
						inspectorNumber:3,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						townShips:['小榄镇','东升镇','南头镇'],
						tags:['起重机','法定检验','年度检验']
					},
					{
						id:Math.round(Math.random()*1000),
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社1-待检测',
						eNum:7,
						inspectorNumber:3,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						townShips:['小榄镇','东升镇','南头镇'],
						tags:['起重机','法定检验','年度检验']
					},
					{
						id:Math.round(Math.random()*1000),
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社1-待检测',
						eNum:7,
						inspectorNumber:3,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						townShips:['小榄镇','东升镇','南头镇'],
						tags:['起重机','法定检验','年度检验']
					}
				]
				
				callBack && callBack();
				return tempTaskArr;
			}
		},
		components:{
			'task-item':taskItem,
			'uni-icons':uniIcons,
			'uni-search-bar':uniSearchBar
		},
		//下拉加载数据（模拟）
		onReachBottom() {
			console.log('触底了');
			
			var tempTaskArr1 = this.getTaskItem();
			//虚拟三页
			
			
			if(this.taskPageIndex < 3){
				this.taskArr = [...this.taskArr,...tempTaskArr1];
				this.taskPageIndex++;
			}else{
				this.noMoreTask = true
			}
			
		},
		//上拉刷新
		onPullDownRefresh(){
			this.taskArr = [];
			this.noMoreTask = false;
			this.taskPageIndex  = 1;
			setTimeout(()=>{
				this.taskArr = this.getTaskItem(()=>{
					uni.stopPullDownRefresh()
				});
			},1000)
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
.index-tab{
	display: flex;
	flex-direction: row;
	justify-content: flex-start;
	background-color:#3291F8 ;
	/* background-color:#ff0000; */
	color:#ffffff;
	font-size:28rpx;
	font-weight:bold;
	height:100rpx;
	line-height:100rpx;
	border-top:2rpx solid #6495ED;
	width:100%;
	
}
.index-tab .tabitem{
	height:80rpx;
	line-height:80rpx;
	width:90rpx;
	margin:0 20rpx;
	text-align: center;
}
.index-tab .tabitem.active{
	border-bottom:4rpx solid #ffffff;
}
.index-tab .search{
	flex-grow:1;text-align: right;padding-right:20rpx;
}
.index-tab .search-tab{
	display:none;
}
.index-tab .search-input{
	background-color: #ffffff;
	font-weight:normal;
	border-radius:40rpx;
	text-indent: 20rpx;
	margin:auto 0;
	width:80%;
	color:#666666;
	height:70rpx;
}
.index-tab .search-bar{
	display: none;
}
.index-tab .search-bar2{
	display:flex;
	width:100%;
	background-color:#3291F8;
	color:#ffffff !important;
	font-weight:normal;
	
	/* font-weight:normal; */
}
.index-tab uni-text.uni-searchbar__cancel{
	color:#ffffff !important;
}
.no-more-task{
	height:100rpx;
	width:100%;
	display: block;
	line-height:100rpx;
	color:#aeaeae;
	text-align: center;
	font-size:28rpx;
}
</style>
