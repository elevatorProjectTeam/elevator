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
			<block v-if="currentTab.id == tab.id" v-for="(taskItem) in taskArr" :key="taskItem.id">
				<task-item :taskItem="taskItem" :currentTab="currentTab">
					<block slot="button">
						<view  class="button-container"  v-if="currentTab.button" style="z-index:999">
							<button size="mini" class="e-button" plain="true" @click.stop="toDetail(taskItem.id)" v-if="currentTab.button">{{currentTab.button}}</button>
						</view>
					</block>
					
				</task-item>
			</block>
		</block>
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
				
				taskArr:[
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
					{
						id:2,
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
						id:3,
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
						id:4,
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
						id:5,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社1-待检测',
						eNum:7,
						inspectorNumber:3,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						townShips:['小榄镇','东升镇','南头镇'],
						tags:['起重机','法定检验','年度检验']
					},
				],
				taskArr2:[
					{
						id:1,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社1-待评价',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:2,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社222',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:3,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社333',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:4,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社44',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:5,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社55',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
				],
				taskArr3:[
					{
						id:1,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社1-已完成',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:2,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社222',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:3,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社333',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:4,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社44',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
					{
						id:5,
						src:"/static/images/temp/temp1.png",
						orgName:'竹源股份合作经济联合社55',
						eNum:5,
						address:'中山市小榄镇竹源路36号',
						time:'2019-08-16',
						tags:['电梯','法定检验','年度检验']
					},
				]
			}
		},
		onLoad() {
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
			
			uni.setStorage({
				key:'currentTab',
				data:this.userTab[0]
			});
			this.currentTab = this.userTab[0]
			
		},
		methods: {
			toDetail(id){
				uni.navigateTo({
					url:'/pages/taskDetail/taskDetail?id='+id,
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
			}
		},
		components:{
			'task-item':taskItem,
			'uni-icons':uniIcons,
			'uni-search-bar':uniSearchBar
			
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
</style>
