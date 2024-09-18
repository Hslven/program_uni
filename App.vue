<script>
export default {
    data() {
        return {};
    },
    onLaunch: function () {
        try {
            this.globalData.userInfo = JSON.parse(uni.getStorageSync('userInfo'));
            this.globalData.token = uni.getStorageSync('token');
        } catch (e) {
            console.log('CatchClause', e);
            console.log('CatchClause', e);
            console.log(e);
        }
    },
    globalData: {
        userInfo: {
            nickname: '点击登录',
            avatar: 'http://yanxuan.nosdn.127.net/8945ae63d940cc42406c3f67019c5cb6.png'
        },
        token: ''
    }
};
</script>
<style>
/**app.wxss**/
.container {
    box-sizing: border-box;
    background-color: #f4f4f4;
    font-family: PingFangSC-Light, helvetica, 'Heiti SC';
}

view,
image,
text,
navigator {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}

view,
text {
    font-family: PingFangSC-Light, helvetica, 'Heiti SC';
    font-size: 29rpx;
    color: #333;
}
</style>
