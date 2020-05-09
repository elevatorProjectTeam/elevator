<template>
	<view>
		<block v-for="(item,index) in equipInfo1.list" :key="index">
			<task-form-item :item="item"></task-form-item>
		</block>
		<button class="ed-btn" v-if="type=='waitingTest'" @click="startTest">开始检测</button>
		<button class="ed-btn" v-if="type=='waitingTest'" @click="addDifficult">加入疑难单</button>
		<button class="ed-btn" v-if="type=='ongoing'" @click="finish">完成</button>
	</view>
</template>

<script>
	import taskFormItem from '@/components/taskFormItem.vue'
	export default {
		data() {
			return {
				type:'waitingTest',//waitingTest,difficult
				equipInfo1:{
					id:'equitmentCondition',
					title:'设备概况',
					list:[{
						label:'维保单位',
						value:'中山市广日电梯工程有限公司'
					},{
						label:'使用单位',
						value:'中山市小榄镇绩东二经济联合社'
					},{
						label:'单位内编号',
						value:'(H-10120)'
					},{
						label:'检验类型',
						value:'定期检验'
					},{
						label:'联系电话',
						value:'180000000000'
					},
					{
						label:'单位地址',
						value:'中山市小榄镇XX路xx号'
					},{
						label:'检验时间',
						value:'2018-06-07'
					},{
						label:'检验人员',
						value:'张三、李四'
					},]
					
				},
				
			}
		},
		methods: {
			startTest(){
				this.type='ongoing'
			},
			addDifficult(){
				uni.navigateTo({
					url:'/pages/difficultReason/difficultReason',
					success(res){
						// console.log(res)
					}
				})
			},
			finish(){
				
			}
		},
		components:{
			taskFormItem
		}
	}
</script>

<style>
.ed-btn{
	width:80%;
	background-color: #3291F8;
	color:#ffffff;
	border-radius:50rpx;
	margin-top:30rpx;
}
</style>
