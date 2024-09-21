<template>
  <view class="container">
    <view class="upload-section">
      <button @click="uploadContract">上传合同</button>
      <view class="image-list">
        <image
          v-for="(image, index) in contractImages"
          :key="index"
          :src="image"
          mode="aspectFit"
          style="width: 100%; margin-top: 10px;"
        />
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      contractImages: [] // 存储上传的合同图片列表
    };
  },
  methods: {
    uploadContract() {
      uni.chooseImage({
        count: 6 - this.contractImages.length, // 允许选择的图片数量
        success: (res) => {
          this.contractImages = this.contractImages.concat(res.tempFilePaths); // 添加新上传的图片
        }
      });
    }
  }
};
</script>

<style>
.container {
  padding: 20px;
}
.upload-section {
  margin-top: 20px;
}
.image-list {
  margin-top: 20px;
}
</style>