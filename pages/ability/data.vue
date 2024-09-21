<template>
  <view class="charts-box">
    <qiun-data-charts type="column" :chartData="barChartData" />
    <qiun-data-charts type="pie" :chartData="pieChartData" />
  </view>
</template>

<script>
export default {
  data() {
    return {
      barChartData: {
        categories: [], // 日期
        series: [
          {
            name: "车辆租出",
            data: [] // 租出数量
          },
          {
            name: "合同成交",
            data: [] // 成交数量
          }
        ]
      },
      pieChartData: {
        series: [
          {
            name: "租借状态",
            data: [] // 租借状态数据
          }
        ]
      }
    };
  },
  onReady() {
    this.getServerData();
  },
  methods: {
    getServerData() {
      // 模拟从服务器获取数据时的延时
        // 柱状图数据
        let barRes = {
          categories: ["2024-01", "2024-02", "2024-03", "2024-04", "2024-05", "2024-06"],
          series: [
            {
              name: "车辆租出",
              data: [20, 30, 25, 40, 35, 50] // 示例数据
            },
            {
              name: "合同成交",
              data: [15, 25, 20, 30, 28, 45] // 示例数据
            }
          ]
        };

        // 饼图数据
        let pieRes = {
          series: [
            {
              name: "租借状态",
              data: [
                { name: "已租出", value: 120 },
                { name: "待租出", value: 80 },
                { name: "已归还", value: 50 },
                { name: "逾期未归还", value: 10 }
              ]
            }
          ]
        };

        // 更新数据
        this.barChartData.categories = barRes.categories;
        this.barChartData.series = barRes.series;
        this.pieChartData.series = pieRes.series;
    }
  }
};
</script>

<style scoped>
.charts-box {
  width: 100%;
  height: auto;
  margin-bottom: 20px;
}
</style>