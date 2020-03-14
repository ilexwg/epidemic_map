<template>
  <div class="about">
    <div class="chart">
    </div>
  </div>
</template>

<script>
import echarts from 'echarts';

export default {
  name: 'About',
  methods: {
    init() {
      const myChart = echarts.init(document.querySelector('.chart'));
      const option = {
        title: {
          text: '全国新增确诊/疑似趋势'
        },
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['新增确诊', '新增疑似']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },
        xAxis: {
          type: 'category',
          data: ['2.11', '2.12', '2.13', '2.14', '2.15', '2.16', '2.17', '2.18','2.19', '2.20', '2.21', '2.22', '2.23']
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            name: '新增确诊',
            type: 'line',
            smooth: true,
            data: [2022, 15153, 5093, 2644, 2009, 2051, 1891, 1751, 825, 892, 399, 649, 416]
          },
          {
            name: '新增疑似',
            type: 'line',
            smooth: true,
            data: [3342, 2007, 2450, 2277, 1918, 1563, 1432, 1185, 1277, 1614, 1614, 882, 620]
          }
        ]
      };

      myChart.setOption(option);
    }
  },
  mounted() {
    this.init();
  }
};
</script>

<style lang="less" scoped>
.about {
  width: 100%;
  height: 100%;
  padding: 30px;

  .chart {
    width: 80%;
    height: 50%;
    margin: 0 auto;
    padding: 10px;
    border-radius: 6px;
    background-color: #f2f2f2;
  }
}
</style>
