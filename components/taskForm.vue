<template>
	<view style="">
		<block v-for="(item,index) in taskForm" :key="item.id">
			<view class="fForm-container">
				<view class="tForm-title">{{item.title}}</view>
				<block v-for="(second,secondI) in item.list" :key="secondI">
					<form-item :item="second">
						<view slot="formRight">
							<!-- 一些特殊的右边 -->
							<!-- 复制 -->
							<block v-if="second.slot && second.slot=='复制'">
								{{second.value}}|<text style="color:#007AFF" @click="copy(second.value)">{{second.slot}}</text>
							</block>
							<!-- 打电话 -->
							<block v-if="second.slot && second.slot=='打电话'">
								{{second.value}}|<text style="color:#007AFF" @click="makePhone(second.value)">{{second.slot}}</text>
							</block>
							<!-- 检测员 -->
							<block v-if="second.slot && second.slot=='选择'">
								{{second.value}}
							</block>
							<!-- 日历 -->
							<block v-if="second.slot && second.slot=='calendar'">
								{{second.value}}|<text style="color:#007AFF" @click="open">更改</text>
								<uni-calendar 
								    ref="calendar"
								    :insert="false"
									:date="second.value"
									v-model = "second.value"
									:data-obj="second"
								    @confirm="confirm"
								     ></uni-calendar> 
							</block>
							<!-- 评分 -->
							<block v-if="second.slot && second.slot=='grade'">
								<uni-rate max="5" size="12" :value="second.value" disabled="true" style="height:100%;padding-top:30rpx;"></uni-rate>
							</block>
						</view>
					</form-item>
			
				</block>
			</view>
		</block>
	</view>
</template>

<script>
	import formItem from '@/components/taskFormItem.vue'; //单项信息
	import uniCalendar from '@/components/uni-calendar/uni-calendar.vue'; //日期组件
	import uniRate from '@/components/uni-rate/uni-rate.vue';  //评分组件
	export default {
		data() {
			return {
				
			};
		},
		created(){
			// console.log("created",this.taskForm)
		},
		mounted(){
			// console.log("mounted",this.taskForm)
		},
		props:['taskForm'],
		components:{
			formItem,
			'uni-calendar':uniCalendar,
			'uni-rate':uniRate
		},
		methods:{
			copy(_data){
				console.log('aaa')
				// #ifdef MP
				uni.setClipboardData({
				    data: _data,
				    success: function () {
				        console.log('success',_data);
				    }
				});
				// #endif
			},
			makePhone(_data){
				uni.makePhoneCall({
				    phoneNumber: _data, //仅为示例
					complete:function(){
						console.log('phonesuccess',_data)
					}
				});
			},
			open(){
				var can=this.$refs.calendar;
				can[0].open();
				this.tempDate = this.$refs.calendar.date;
			},
			confirm(e) {
				this.tempDate = e.fullDate;
				
				console.log(this.$refs.calendar[0].$attrs['data-obj'].value)
				
			}
		}
	}
</script>

<style>
.fForm-container{
	margin:0 auto;
	margin-bottom:20px;
	width:calc(100vw - 20rpx);
	padding:10rpx 10rpx 0 10rpx;
	font-size:28rpx;
	background-color: #ffffff;
}
.tForm-title{
	font-size:32rpx;
	font-weight:bold;
	height:80rpx;
	line-height:80rpx;
	color:#000000;
}
.container-s{
	height:80rpx;
	line-height:80rpx;
	flex-direction: row;
	justify-content: space-between;
	border-bottom:1px solid #cccccc;
	margin-top:2px;
}
.container-s-label{
	height:50rpx;
	/* background-color: #007AFF; */
}

.container-s-value{
	height:50rpx;
	text-align: right;
	color:#000000;
	display: flex;
	flex-direction: row;
	/* background-color: #4CD964; */
	font-weight:bold;
	
}
</style>
