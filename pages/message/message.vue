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
  @font-face {
    font-family: "iconfont";
    src: url('~@/static/iconfont-msg/iconfont.ttf');
    /* IE9 */
    src: url('~@/static/iconfont-msg/iconfont.eot') format('embedded-opentype'),
      /* IE6-IE8 */
      url('data:application/x-font-woff2;charset=utf-8;base64,d09GMgABAAAAAAMMAAsAAAAABtgAAAK+AAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAHEIGVgCCcAqBZIFuATYCJAMICwYABCAFhG0HLxsTBsgOJcHMwIABgFBEPPxzP+q+X5NBmdgUTZHHk2ZoQZYbrEIky9aWlhp4zv9fm/t9OUQ8mN21HTHxXMXTICYTbLxOiA5LZWNjMhvZGJn5n8vpXQMokPmBcpl7UC/AeGtAe2MUWYEE4A3Tyxc0kI8JVOuSQbJSVtMCrjJ6VSDOVYpBcM25ZDIWrRSKmoOZRHLASWWymXwDcDv8fvwHebiCRJ6C3rh9VjoCBb/gB9DVcgF6fAR7PgPYMVJMABmxXxvahAQjINUhTh/YV3bwC/5LXyP2+ueJAnRmLeiArHtiO86tliUgc++jG8DFqCvJ67zc3cOnHx9bnp5aX17an5/bnDEjZuQZNeu6FmzbjkX7lhW80OHW2HoUaHksuXuOOzxxv/YsaNjEowv3HlRk5y4vObuh+3RP9jLNc3Bzx+j7A4L8O5gOZXcxPU789BsKUoKTh/RChdBo6HDS0S54dqWfNpdbDvDm0/RoT9+kGJ/6MdIMzcZP4dGYJF8oACifo7eo6Cf/xs+wHNTvk/NX6cEB/Hj3jwod5XNOPwuovBVN+KWiLN+SCa4OJRnQUhtIbHC61apq1SghW7PvsbK2+4+FSm1vYanQmUKq0gCa4ScgV2MSCpXmodq48uM1WlBIZG7AmFUAodEtJOq9hFSjezTDf0Gu3S8UGgNBtcMIuLDGUKjciykZZGQED01i1bBBL1otc4+ym4hiVDtIs9yQ2EaoWeXFMl5ajJYTPaFzbDGPKeSMiVikBh0uA88RrdaAjdSgJsOMVzJmzBIEse5N/LBBB+6WUcQghhiBDZmEqQwz0BP9zox76fNNCIVRWoNoS1NO24agzFTjYzI8aQ+0XKTv1XQvr5iNUZBjGBEmogx0sDIwj9DSMsCM9fPUiGEMTzkiYJRFMO3EviJ+fYnu63ZBNS1PwsxAkF/RqbQEAAAA') format('woff2'),
      url('~@/static/iconfont-msg/iconfont.woff') format('woff'),
      url('~@/static/iconfont-msg/iconfont.ttf') format('truetype'),
      /* chrome, firefox, opera, Safari, Android, iOS 4.2+ */
      url('~@/static/iconfont-msg/iconfont.svg') format('svg');
    /* iOS 4.1- */
  }

  .iconfont {
    font-family: "iconfont" !important;
    font-size: 36rpx;
    font-style: normal;
    text-align: center;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    display: inline-block;
  }

  .icon-smile:before {
    content: "\e600";
    color: #1890FF;
  }

  .icon-smile {
    width: 100rpx;
    height: 100%;
  }

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
