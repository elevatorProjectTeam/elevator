<template>
  <view class="msg-container">
    <view class="msg-item" v-for="(msg, index) in msgArr.slice(sliceStart,sliceEnd)" :key="index">
      <i class="iconfont icon-smile"></i>
      <view style="msg-text">
        <view class="msg-title">{{msg.title}}</view>
        <view class="msg-content">{{msg.content}}</view>
      </view>
    </view>
    <uni-pagination show-icon="true" :total="msgTotal" current="1" pageSize="5" @change="change"></uni-pagination>
  </view>
</template>

<script>
  import uniPagination from '@/components/uni-pagination/uni-pagination.vue'
  export default {
    components: {
      uniPagination
    },
    data() {
      return {
        msgArr: [{
            title: "1 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          },
          {
            title: "2 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          },
          {
            title: "3 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          },
          {
            title: "4 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          },
          {
            title: "5 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          }, {
            title: "6 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          },
          {
            title: "7 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          },
          {
            title: "8 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          },
          {
            title: "9 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          },
          {
            title: "10 中山**花园23栋",
            content: "**地址，**产品5套发出检修申请。"
          }
        ],
        msgTotal: 10,
        current: 1,
        sliceStart: 0,
        sliceEnd: 5,
      }
    },

    methods: {
      change(e) {
        // console.log(e)
        this.current = e.current
        this.sliceStart = e.sliceStart
        this.sliceEnd = e.sliceEnd
      }
    }
  }
</script>

<style>


  .msg-container {
    width: 100vw;
    height: calc(100vh - 100rpx);
    background-color: #F8F8F8;
    overflow: auto;
  }

  .msg-item {
    width: 100vw;
    height: calc((100vh - 38vh)/5);
    background-color: white;
    box-shadow: 0rpx 8rpx 14rpx rgba(0, 0, 0, 0.15);
    padding: 20rpx 0;
    margin-bottom: 20rpx;
    display: flex;
  }

  .msg-title {
    font-size: 32rpx;
  }

  .msg-content {
    font-size: 28rpx;
    color: #595959;
    margin-top: 10rpx;
  }
</style>
