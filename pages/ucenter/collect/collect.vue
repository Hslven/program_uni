<template>
    <view class="container">
        <view class="collect-list">
            <view class="item" @tap="openGoods" @touchstart="touchStart" @touchend="touchEnd" :data-index="index" v-for="(item, index) in collectList" :key="item.id">
                <image class="img" :src="item.list_pic_url"></image>

                <view class="info">
                    <view class="name">{{ item.name }}</view>
                    <view class="subtitle">{{ item.goods_brief }}</view>
                    <view class="price">￥{{ item.retail_price }}</view>
                </view>
            </view>
        </view>
    </view>
</template>

<script>
var util = require('../../../utils/util.js');
var api = require('../../../config/api.js');
var app = getApp();
export default {
    data() {
        return {
            typeId: 0,
            collectList: [],
            touch_start: '',
            touch_end: ''
        };
    },
    onLoad: function (options) {
        this.getCollectList();
    },
    onReady: function () {},
    onShow: function () {},
    onHide: function () {
        // 页面隐藏
    },
    onUnload: function () {
        // 页面关闭
    },
    methods: {
        getCollectList() {
            let that = this;
            util.request(api.CollectList, {
                typeId: that.typeId
            }).then(function (res) {
                if (res.errno === 0) {
                    console.log(res.data);
                    that.setData({
                        collectList: res.data.data
                    });
                }
            });
        },

        openGoods(event) {
            let that = this;
            let goodsId = this.collectList[event.currentTarget.dataset.index].value_id;

            //触摸时间距离页面打开的毫秒数
            var touchTime = that.touch_end - that.touch_start;
            console.log(touchTime);
            //如果按下时间大于350为长按
            if (touchTime > 350) {
                uni.showModal({
                    title: '',
                    content: '确定删除吗？',
                    success: function (res) {
                        if (res.confirm) {
                            util.request(
                                api.CollectAddOrDelete,
                                {
                                    typeId: that.typeId,
                                    valueId: goodsId
                                },
                                'POST'
                            ).then(function (res) {
                                if (res.errno === 0) {
                                    console.log(res.data);
                                    uni.showToast({
                                        title: '删除成功',
                                        icon: 'success',
                                        duration: 2000
                                    });
                                    that.getCollectList();
                                }
                            });
                        }
                    }
                });
            } else {
                uni.navigateTo({
                    url: '/pages/goods/goods?id=' + goodsId
                });
            }
        },

        //按下事件开始
        touchStart: function (e) {
            let that = this;
            that.setData({
                touch_start: e.timeStamp
            });
            console.log(e.timeStamp + '- touch-start');
        },

        //按下事件结束
        touchEnd: function (e) {
            let that = this;
            that.setData({
                touch_end: e.timeStamp
            });
            console.log(e.timeStamp + '- touch-end');
        }
    }
};
</script>
<style>
page {
    background: #f4f4f4;
    min-height: 100%;
}

.container {
    background: #f4f4f4;
    min-height: 100%;
}

.collect-list {
    width: 100%;
    height: auto;
    overflow: hidden;
    background: #fff;
    padding-left: 30rpx;
    border-top: 1px solid #e1e1e1;
}

.item {
    height: 212rpx;
    width: 720rpx;
    background: #fff;
    padding: 30rpx 30rpx 30rpx 0;
    border-bottom: 1px solid #e1e1e1;
}

.item:last-child {
    border-bottom: 1px solid #fff;
}

.item .img {
    float: left;
    width: 150rpx;
    height: 150rpx;
}

.item .info {
    float: right;
    width: 540rpx;
    height: 150rpx;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding-left: 20rpx;
}

.item .info .name {
    font-size: 28rpx;
    color: #333;
    line-height: 40rpx;
}

.item .info .subtitle {
    margin-top: 8rpx;
    font-size: 24rpx;
    color: #888;
    line-height: 40rpx;
}

.item .info .price {
    margin-top: 8rpx;
    font-size: 28rpx;
    color: #333;
    line-height: 40rpx;
}
</style>
