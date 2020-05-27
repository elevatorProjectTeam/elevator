<template>
	<view>
		<task-form-item :item="equipInfo1.maintenanceUnit"></task-form-item>
		<task-form-item :item="equipInfo1.user"></task-form-item>
		<task-form-item :item="equipInfo1.no"></task-form-item>
		<task-form-item :item="equipInfo1.type"></task-form-item>
		<task-form-item :item="equipInfo1.tel"></task-form-item>
		<task-form-item :item="equipInfo1.address"></task-form-item>
		<task-form-item :item="equipInfo1.time"></task-form-item>
		<task-form-item :item="equipInfo1.member"></task-form-item>
		<!-- <block v-for="(item,index) in equipInfo1.list" :key="index">
			<task-form-item :item="item">
				<view slot="formRight">
					
					<block v-if="item.slot && item.slot=='array'">
						<block v-for="(v,index) in item.value" :key="index">
							{{v}},
						</block>
					</block>
				</view>
			</task-form-item>
		</block> -->
		<button class="ed-btn" v-if="type=='waitingTest'" @click="startTest">开始检测</button>
		<button class="ed-btn" v-if="type=='waitingTest'" @click="addDifficult">加入疑难单</button>
		<button class="ed-btn" v-if="type=='ongoing'" @click="finish">完成</button>
		<view>
			<zhilin-picker
			    v-model="show"
			    :dataArr="membersArr"
			    @change="onChange"
				@confirm="onConfirm"
				:initSelected="initSelected"
			/>
		</view>
	</view>
</template>

<script>
	import taskFormItem from '@/components/taskFormItem.vue'
	import zhilinPicker from "@/components/zhilin-picker/zhilin-picker.vue"
	export default {
		data() {
			return {
				
				show:false,
				title:'选择检测员',
				membersArr:['张三','李四','刘一','王二','陈五','赖六','何七','梁八'],
				initSelected:['张三'],
				
				type:'waitingTest',//waitingTest,difficult
				equipInfo1:{
					id:'equitmentCondition',
					title:'设备概况',
					maintenanceUnit:{
						id:'maintenanceUnit',
						label:'维保单位',
						value:'中山市广日电梯工程有限公司'
					},
					user:{
						id:'user',
						label:'使用单位',
						value:'中山市小榄镇绩东二经济联合社'
					},
					no:{
						id:'no',
						label:'单位内编号',
						value:'H-10120'
					},
					type:{
						id:'type',
						label:'检验类型',
						value:'定期检验'
					},
					tel:{
						id:'tel' ,
						label:'联系电话',
						value:'18000000000',
					},
					address:{
						id:'address',
						label:'单位地址',
						value:'中山市小榄镇XX路xx号'
					},
					time:{
						id:'time',
						label:'检验时间',
						value:'2018-06-07'
					},
					member:{
						id:'member',
						label:'检验人员',
						value:'张三,李四'
						
					}
				},
				
			}
		},
		methods: {
			startTest(){
				this.show=true;
				// console.log('dasfdsa',this.equipInfo1.member.value.split(','))
				this.initSelected=this.equipInfo1.member.value.split(',');
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
				
			},
			onChange(e){
				console.log('change',e);
				this.equipInfo1.member.value=e
			},
			onConfirm(){
				this.type='ongoing'
			}
		},
		components:{
			taskFormItem,zhilinPicker 
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
.uni-list-cell {
justify-content: flex-start
}
</style>
