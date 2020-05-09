<template>
  <view class="info-container">
    <view class="info-item" v-for="(item, index) in infoArr" :key="index">
      <view class="info-title">{{item.title}}</view>
      <view class="info-text">{{item.info}}</view>
      <i class="iconfont icon-jiantou"></i>
    </view>
  </view>
</template>

<script>
  export default {
    data() {
      return {
        infoArr: [{
            title: '科室名称',
            info: '竹源股份合作经济联合社'
          },
          {
            title: '组名',
            info: '检测组001'
          },
          {
            title: '姓名',
            info: '何先生'
          },
          {
            title: '岗位',
            info: '检测员'
          },
          {
            title: '电话',
            info: '13800000000'
          },
          {
            title: '单位地址',
            info: '中山市小榄镇竹源路36号'
          }
        ],
      }
    }
  }
</script>

<style>
  .info-container {
    width: 100vw;
  }

  .info-item {
    width: calc(100vw-40rpx);
    height: 100rpx;
    font-size: 30rpx;
    line-height: 100rpx;
    background-color: #FFFFFF;
    padding: 0 20rpx;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .info-title {
    flex-grow: 1;
    margin-left: 10rpx;
  }

  .info-text {
    color: #A6A4A4;
    padding-right: 10rpx;
  }

  .iconfont {
    font-family: "iconfont" !important;
    font-size: 36rpx;
    font-style: normal;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    display: inline-block;
  }

  .icon-jiantou:before {
    content: "\e621";
    color: #A6A4A4;
  }
</style>
