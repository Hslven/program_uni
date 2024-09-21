<template>
  <!-- index.wxml -->
  <view class="container">
    <!-- 搜索 -->
    <!-- <view class="search">
            <navigator url="/pages/search/search" class="input">
                <image class="icon"></image>
                <text class="txt">商品搜索, 共{{ goodsCount }}款好物</text>
            </navigator>
        </view>
        <swiper class="banner" :indicator-dots="true" :autoplay="true" interval="3000" duration="1000">
            <swiper-item v-for="(item, index) in banner" :key="item.id">
                <navigator :url="item.link">
                    <image :src="item.image_url" background-size="cover"></image>
                </navigator>
            </swiper-item>
        </swiper>
    </view> -->
    <!-- 标签 -->
    <!-- <view class="m-menu">
            <navigator class="item" :url="item.url" v-for="(item, index) in channel" :key="item.id">
                <image :src="item.icon_url" background-size="cover"></image>

                <text>{{ item.name }}</text>
            </navigator>
        </view> -->
    <view class="a-section a-brand">
      <view class="h">
        <!-- <navigator url="../brand/brand"> -->
        <text class="txt">功能统计</text>
        <!-- </navigator> -->
      </view>
      <view class="b">
        <view class="item item-1" v-for="(item, index) in brand" :key="item.id"
        @click="navigatorTo(item.url)"
        >
          <!-- <navigator :url="'/pages/brandDetail/brandDetail?id=' + item.id"> -->
          <!-- </navigator> -->
          <view class="wrap">
            <view
              class="img"
              :style="{ 'background-color': item.color }"
            >
              <image
                :src="item.new_pic_url"
                background-size="cover"
                style="width: 40%; height: 60%; position: absolute; right: 0; bottom: 0px"
              ></image>
            </view>
            <view class="mt">
              <text class="brand">{{ item.name }}</text>
              <!-- <text class="price">{{ item.floor_price }}</text> -->
              <!-- <text class="unit">元起</text> -->
            </view>
          </view>
        </view>
      </view>
    </view>
    <!-- <view class="a-section a-new" v-if="newGoods.length > 0">
            <view class="h">
                <view>
                    <navigator url="../newGoods/newGoods">
                        <text class="txt">周一周四 · 新品首发</text>
                    </navigator>
                </view>
            </view>
            <view class="b">
                <view class="item" v-for="(item, index) in newGoods" :key="item.id">
                    <navigator :url="'../goods/goods?id=' + item.id">
                        <image class="img" :src="item.list_pic_url" background-size="cover"></image>
                        <text class="name">{{ item.name }}</text>
                        <text class="price">￥{{ item.retail_price }}</text>
                    </navigator>
                </view>
            </view>
        </view> -->
    <!-- <view class="a-section a-popular" v-if="hotGoods.length > 0">
            <view class="h">
                <view>
                    <navigator url="../hotGoods/hotGoods">
                        <text class="txt">人气推荐</text>
                    </navigator>
                </view>
            </view>
            <view class="b">
                <view class="item" v-for="(item, index) in hotGoods" :key="item.id">
                    <navigator :url="'/pages/goods/goods?id=' + item.id">
                        <image class="img" :src="item.list_pic_url" background-size="cover"></image>
                        <view class="right">
                            <view class="text">
                                <text class="name">{{ item.name }}</text>
                                <text class="desc">{{ item.goods_brief }}</text>
                                <text class="price">￥{{ item.retail_price }}</text>
                            </view>
                        </view>
                    </navigator>
                </view>
            </view>
        </view> -->
    <!-- <view class="a-section a-topic" v-if="'topics.length > 0'">
            <view class="h">
                <view>
                    <navigator url="../topic/topic" open-type="switchTab">
                        <text class="txt">专题精选</text>
                    </navigator>
                </view>
            </view>
            <view class="b">
                <scroll-view :scroll-x="true" class="list">
                    <view class="item" v-for="(item, index) in topics" :key="item.id">
                        <navigator :url="'../topicDetail/topicDetail?id=' + item.id">
                            <image class="img" :src="item.scene_pic_url" background-size="cover"></image>
                            <view class="np">
                                <text class="name">{{ item.title }}</text>
                                <text class="price">￥{{ item.price_info }}元起</text>
                            </view>
                            <text class="desc">{{ item.subtitle }}</text>
                        </navigator>
                    </view>
                </scroll-view>
            </view>
        </view> -->
    <!-- <view class="good-grid" v-for="(item, index) in floorGoods" :key="item.id">
            <view class="h">
                <view>
                    <text>{{ item.name }}</text>
                </view>
            </view>

            <view class="b">
                <block v-for="(iitem, iindex) in item.goodsList" :key="iitem.id">
                    <navigator :url="'../goods/goods?id=' + iitem.id" class="item">
                        <image class="img" :src="iitem.list_pic_url" background-size="cover"></image>
                        <view class="name">{{ iitem.name }}</view>
                        <view class="price">￥{{ iitem.retail_price }}</view>
                    </navigator>
                </block>
            </view>
        </view> -->
  </view>
</template>

<script>
const util = require('../../utils/util.js');
const api = require('../../config/api.js');
const user = require('../../services/user.js');

//获取应用实例
const app = getApp();
export default {
  data() {
    return {
      goodsCount: 0,
      newGoods: [],
      hotGoods: [],
      topics: [],
      brands: [],
      floorGoods: [],
      banner: [],
      channel: [],
      brand: [
        {
          id: 1026000,
          name: '合同上传',
          list_pic_url: 'http://yanxuan.nosdn.127.net/658f09b7ec522d31742b47b914d64338.png',
          simple_desc:
            '严选寻访Calvin Klein品牌的制造商，\n深入世界领带第一生产地，设计与品质并重，\n致力于给消费者带来优质典雅的服饰用品。',
          pic_url: 'http://yanxuan.nosdn.127.net/fb139c9f11a10deb41beeb42aaad488e.png',
          sort_order: 1,
          is_show: 1,
          floor_price: 39,
          app_list_pic_url: 'http://yanxuan.nosdn.127.net/658f09b7ec522d31742b47b914d64338.png',
          is_new: 1,
          // new_pic_url: 'http://yanxuan.nosdn.127.net/76638fb8e6990aadf837ce761c3b7399.jpg',
          new_pic_url: 'https://api.iconify.design/line-md:briefcase-twotone.svg?color=tan',
          new_sort_order: 1,
          color: '#dfe4e8',
          url: '/pages/ability/contract',
        },
        {
          id: 1001000,
          app_list_pic_url: 'http://yanxuan.nosdn.127.net/1541445967645114dd75f6b0edc4762d.png',
          floor_price: 12.9,
          id: 1001000,
          is_new: 1,
          is_show: 1,
          list_pic_url: 'http://yanxuan.nosdn.127.net/1541445967645114dd75f6b0edc4762d.png',
          name: '数据分析',
          new_sort_order: 2,
          pic_url: 'http://yanxuan.nosdn.127.net/4ea3f1e60dd77c45c218e503d721a1ed.jpg',
          // new_pic_url: 'http://yanxuan.nosdn.127.net/4ea3f1e60dd77c45c218e503d721a1ed.jpg',
          new_pic_url:
            'https://api.iconify.design/line-md:document-report-twotone.svg?color=%23888888',
          simple_desc:
            '严选精选了MUJI制造商和生产原料，↵用几乎零利润的价格，剔除品牌溢价，↵让用户享受原品牌,的品质生活。',
          sort_order: 2,
          color: '#e9eef0',
          url: '/pages/ability/data',
        },
        {
          app_list_pic_url: 'http://yanxuan.nosdn.127.net/2018e9ac91ec37d9aaf437a1fd5d7070.png',
          floor_price: 9.9,
          id: 1024000,
          is_new: 1,
          is_show: 1,
          list_pic_url: 'http://yanxuan.nosdn.127.net/2018e9ac91ec37d9aaf437a1fd5d7070.png',
          name: '车辆状况',
          new_sort_order: 3,
          pic_url: 'http://yanxuan.nosdn.127.net/2a2ae0d49043e525db8d0d8d84460ac8.png',
          simple_desc:
            '严选找寻德国百年高端厨具WMF的制造商，↵选择拥有14年经验的不锈钢生产工厂，↵为你甄选事半功倍的优质厨具。',
          sort_order: 8,
          // new_pic_url: 'http://yanxuan.nosdn.127.net/abcfa79205679db51198adc19c184dd1.jpg',
          new_pic_url: 'https://api.iconify.design/line-md:cog-filled.svg?color=burlywood',
          color: '#f4f4f4',
          url: '/pages/ability/car',
        },
        {
          app_list_pic_url: 'http://yanxuan.nosdn.127.net/1b1cc16135fd8467d40983f75f644127.png',
          floor_price: 49,
          id: 1001038,
          is_new: 1,
          is_show: 1,
          list_pic_url: 'http://yanxuan.nosdn.127.net/1b1cc16135fd8467d40983f75f644127.png',
          name: '今日收益总欠款',
          new_sort_order: 10,
          pic_url: 'http://yanxuan.nosdn.127.net/c933a662bb79b2a47280363e35ab994b.png',
          simple_desc:
            '严选为制作高品质高颜值皮具配件，↵由Coach、MK等品牌制造商生产，↵由严选360度全程监制，给你带来优质皮具。',
          sort_order: 3,
          // new_pic_url: 'http://yanxuan.nosdn.127.net/b5cd73d3b310bad02539412f064d4ea1.jpg',
          new_pic_url: 'https://api.iconify.design/line-md:list-indented.svg?color=%23888888',

          color: '#f4f4f4',
          url: '/pages/ability/debt',
          // url: '/pages/brandDetail/brandDetail',
        },
      ],
      item: {
        id: '',
        list_pic_url: '',
        name: '',
        retail_price: '',
      },
    };
  },
  onShareAppMessage: function () {
    return {
      title: 'NideShop',
      desc: '车务助手微信小程序商城',
      path: '/pages/index/index',
    };
  },
  onLoad: function (options) {
    this.getIndexData();
    util.request(api.GoodsCount).then((res) => {
      this.setData({
        goodsCount: res.data.goodsCount,
      });
    });
  },
  onReady: function () {
    // 页面渲染完成
  },
  onShow: function () {
    // 页面显示
  },
  onHide: function () {
    // 页面隐藏
  },
  onUnload: function () {
    // 页面关闭
  },
  methods: {
    navigatorTo(url) {
      uni.navigateTo({
        url,
      });
    },
    getIndexData: function () {
      let that = this;
      util.request(api.IndexUrl).then(function (res) {
        if (res.errno === 0) {
          that.setData({
            newGoods: res.data.newGoodsList,
            hotGoods: res.data.hotGoodsList,
            topics: res.data.topicList,
            // brand: res.data.brandList,
            floorGoods: res.data.categoryList,
            banner: res.data.banner,
            channel: res.data.channel,
          });
        }
      });
    },
  },
};
</script>
<style>
.search {
  height: 88rpx;
  width: 100%;
  padding: 0 30rpx;
  background: #fff;
  display: flex;
  align-items: center;
}

.search .input {
  width: 690rpx;
  height: 56rpx;
  background: #ededed;
  border-radius: 8rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}

.search .icon {
  background: url('http://yanxuan.nosdn.127.net/hxm/yanxuan-wap/p/20161201/style/img/icon-normal/search2-2fb94833aa.png')
    center no-repeat;
  background-size: 100%;
  width: 28rpx;
  height: 28rpx;
}

.search .txt {
  height: 42rpx;
  line-height: 42rpx;
  color: #666;
  padding-left: 10rpx;
  font-size: 30rpx;
}

.banner {
  width: 750rpx;
  height: 417rpx;
}

.banner image {
  width: 100%;
  height: 417rpx;
}

.m-menu {
  display: flex;
  height: 181rpx;
  width: 750rpx;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: space-between;
  background-color: #fff;
}

.m-menu .item {
  flex: 1;
  display: block;
  padding: 20rpx 0;
}

.m-menu image {
  display: block;
  width: 58rpx;
  height: 58rpx;
  margin: 0 auto;
  margin-bottom: 12rpx;
}

.m-menu text {
  display: block;
  font-size: 24rpx;
  text-align: center;
  margin: 0 auto;
  line-height: 1;
  color: #333;
}

.a-section {
  width: 750rpx;
  height: auto;
  overflow: hidden;
  background: #fff;
  color: #333;
  margin-top: 20rpx;
}

.a-section .h {
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: center;
  height: 130rpx;
}

.a-section .h .txt {
  padding-right: 30rpx;
  background: url('http://ac-3yr0g9cz.clouddn.com/2cdba05369e10f934e54.png') right 4rpx no-repeat;
  background-size: 16.656rpx 27rpx;
  display: inline-block;
  height: 36rpx;
  font-size: 33rpx;
  line-height: 36rpx;
}

.a-brand .b {
  width: 750rpx;
  height: auto;
  overflow: hidden;
  position: relative;
}

.a-brand .wrap {
  position: relative;
}

.a-brand .img {
  position: absolute;
  left: 0;
  top: 0;
}

.a-brand .mt {
  position: absolute;
  z-index: 2;
  padding: 27rpx 31rpx;
  left: 0;
  top: 0;
}

.a-brand .mt .brand {
  display: block;
  font-size: 33rpx;
  height: 43rpx;
  color: #333;
}

.a-brand .mt .price,
.a-brand .mt .unit {
  font-size: 25rpx;
  color: #999;
}

.a-brand .item-1 {
  float: left;
  width: 375rpx;
  height: 252rpx;
  overflow: hidden;
  border-top: 1rpx solid #fff;
  margin-left: 1rpx;
}

.a-brand .item-1:nth-child(2n + 1) {
  margin-left: 0;
  width: 374rpx;
}

.a-brand .item-1 .img {
  width: 375rpx;
  height: 253rpx;
}

.a-new .b {
  width: 750rpx;
  height: auto;
  overflow: hidden;
  padding: 0 31rpx 45rpx 31rpx;
}

.a-new .b .item {
  float: left;
  width: 302rpx;
  margin-top: 10rpx;
  margin-left: 21rpx;
  margin-right: 21rpx;
}

.a-new .b .item-b {
  margin-left: 42rpx;
}

.a-new .b .img {
  width: 302rpx;
  height: 302rpx;
}

.a-new .b .name {
  text-align: center;
  display: block;
  width: 302rpx;
  height: 35rpx;
  margin-bottom: 14rpx;
  overflow: hidden;
  font-size: 30rpx;
  color: #333;
}

.a-new .b .price {
  display: block;
  text-align: center;
  line-height: 30rpx;
  font-size: 30rpx;
  color: #b4282d;
}

.a-popular {
  width: 750rpx;
  height: auto;
  overflow: hidden;
}

.a-popular .b .item {
  border-top: 1px solid #d9d9d9;
  margin: 0 20rpx;
  height: 264rpx;
  width: 710rpx;
}

.a-popular .b .img {
  margin-top: 12rpx;
  margin-right: 12rpx;
  float: left;
  width: 240rpx;
  height: 240rpx;
}

.a-popular .b .right {
  float: left;
  height: 264rpx;
  width: 456rpx;
  display: flex;
  flex-flow: row nowrap;
}

.a-popular .b .text {
  display: flex;
  flex-wrap: nowrap;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
  height: 264rpx;
  width: 456rpx;
}

.a-popular .b .name {
  width: 456rpx;
  display: block;
  color: #333;
  line-height: 50rpx;
  font-size: 30rpx;
}

.a-popular .b .desc {
  width: 456rpx;
  display: block;
  color: #999;
  line-height: 50rpx;
  font-size: 25rpx;
}

.a-popular .b .price {
  width: 456rpx;
  display: block;
  color: #b4282d;
  line-height: 50rpx;
  font-size: 33rpx;
}

.a-topic .b {
  height: 533rpx;
  width: 750rpx;
  padding: 0 0 48rpx 0;
}

.a-topic .b .list {
  height: 533rpx;
  width: 750rpx;
  white-space: nowrap;
}

.a-topic .b .item {
  display: inline-block;
  height: 533rpx;
  width: 680.5rpx;
  margin-left: 30rpx;
  overflow: hidden;
}

.a-topic .b .item:last-child {
  margin-right: 30rpx;
}

.a-topic .b .img {
  height: 387.5rpx;
  width: 680.5rpx;
  margin-bottom: 30rpx;
}

.a-topic .b .np {
  height: 35rpx;
  margin-bottom: 13.5rpx;
  color: #333;
  font-size: 30rpx;
}

.a-topic .b .np .price {
  margin-left: 20.8rpx;
  color: #b4282d;
}

.a-topic .b .desc {
  display: block;
  height: 30rpx;
  color: #999;
  font-size: 24rpx;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.good-grid {
  width: 750rpx;
  height: auto;
  overflow: hidden;
  background: #fff;
  margin-top: 20rpx;
}

.good-grid .h {
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: center;
  height: 130rpx;
  font-size: 33rpx;
  color: #333;
}

.good-grid .b {
  width: 750rpx;
  height: auto;
  overflow: hidden;
  padding: 0 20rpx;
}

.good-grid .b .item {
  display: block;
  float: left;
  width: 345rpx;
  margin-bottom: 30rpx;
  height: auto;
  overflow: hidden;
  text-align: center;
}

.good-grid .b .item:nth-child(2n + 1) {
  margin-right: 20rpx;
}

.good-grid .item .img {
  width: 345rpx;
  height: 345rpx;
  background: #f8f8f8;
  margin-bottom: 10rpx;
}

.good-grid .item .name {
  width: 100%;
  overflow: hidden;
  height: 40rpx;
  line-height: 40rpx;
  text-align: center;
  font-size: 30rpx;
  color: #333;
}

.good-grid .item .price {
  width: 100%;
  height: 46rpx;
  line-height: 46rpx;
  text-align: center;
  font-size: 30rpx;
  color: #b4282d;
}
</style>
