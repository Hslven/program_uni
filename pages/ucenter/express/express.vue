<template>
    <view class="container">
        <view class="express-header">
            <view class="left">
                <view class="txt">物流单号：{{ expressInfo.logistic_code }}</view>
                <view class="txt">物流公司：{{ expressInfo.shipper_name }}</view>
                <view class="txt">更新时间：{{ expressInfo.request_time }}</view>
            </view>
            <view class="right" v-if="expressInfo.isFinish === 1">
                <view class="update-btn" @tap="updateExpress">更新物流</view>
            </view>
        </view>
        <view class="express-body">
            <view class="current-icon"></view>
            <view :class="'express-item item-' + index" v-for="(item, index) in expressTraces" :key="index">
                <view class="left"></view>

                <view class="right">
                    <view class="info">{{ item.content }}</view>
                    <view class="time">{{ item.datetime }}</view>
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
            orderId: 1,
            expressInfo: {
                logistic_code: '',
                shipper_name: '',
                request_time: '',
                isFinish: 0
            },
            expressTraces: []
        };
    },
    onLoad: function (options) {
        this.setData({
            orderId: options.id
        });
        this.getExpressInfo();
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
        getExpressInfo() {
            let that = this;
            util.request(api.OrderExpress, {
                orderId: that.orderId
            }).then(function (res) {
                if (res.errno === 0) {
                    that.setData({
                        expressInfo: res.data,
                        expressTraces: res.data.traces
                    });
                }
            });
        },

        updateExpress() {
            this.getExpressInfo();
        }
    }
};
</script>
<style>
page {
    height: 100%;
    width: 100%;
    background: #f4f4f4;
}

.container {
    height: 100%;
    width: 100%;
}

.express-header {
    border-top: 1px solid #d9d9d9;
    width: 100%;
    height: auto;
    overflow: hidden;
    background: #fff;
    display: flex;
    padding: 20rpx 30rpx;
}

.express-header .left {
    flex: 1;
    height: 100%;
}

.express-header .left .txt {
    height: 50rpx;
    line-height: 50rpx;
    overflow: hidden;
    width: 100%;
}

.express-header .right {
    width: 160rpx;
    height: 100%;
    display: flex;
}

.express-header .update-btn {
    margin-top: 47rpx;
    width: 158rpx;
    height: 56rpx;
    line-height: 54rpx;
    overflow: hidden;
    text-align: center;
    border-radius: 8rpx;
    color: #333;
    border: 1px solid #666;
}

.express-body {
    margin-top: 20rpx;
    width: 100%;
    height: auto;
    overflow: hidden;
    background: #fff;
    padding: 30rpx;
    position: relative;
}

.current-icon {
    height: 24rpx;
    width: 24rpx;
    position: absolute;
    top: 30rpx;
    left: 50rpx;
    background: #b4282d;
    border-radius: 24rpx;
}

.express-item {
    height: auto;
    width: 100%;
    overflow: hidden;
    display: flex;
    margin-left: 30rpx;
    border-left: 1px solid #d9d9d9;
}

.express-item .left {
    width: 44rpx;
    height: 100%;
    overflow: hidden;
}

.express-item .right {
    flex: 1;
    height: 100%;
    margin-left: 10rpx;
    padding: 20rpx 0;
    border-bottom: 1px solid #f1f2f4;
}

.express-item.item-0 .right {
    padding-top: 0rpx;
}

.express-item:last-child .right {
    border-bottom: none;
    padding-bottom: 0rpx;
}

.express-item .right .info {
    min-height: 42rpx;
    height: auto;
    overflow: hidden;
    padding-right: 30rpx;
    line-height: 42rpx;
    color: #999;
}

.express-item.item-0 .right .info {
    color: #b4282d;
}

.express-item .right .time {
    min-height: 42rpx;
    height: auto;
    overflow: hidden;
    line-height: 42rpx;
    color: #999;
}

.express-item.item-0 .right .time {
    color: #b4282d;
}
</style>
