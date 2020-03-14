<template>
  <div class="map">
    <div class="map-box"></div>
  </div>
</template>

<script>
import echarts from 'echarts';
import jsonp from 'jsonp';
import 'echarts/map/js/china';

const option = {
  title: {
    text: 'vue实现疫情地图',
    x: 'center',
    textStyle: '#9c0505'
  },
  series: [
    {
      type: 'map',
      map: 'china',
      label: {
        show: true,
        color: 'red',
        fontSize: 10
      },
      itemStyle: {
        borderColor: 'blue',
        borderWidth: 1
      },
      emphasis: {
        label: {
          color: '#a1a2a3',
          fontSize: 12
        },
        itemStyle: {
          areaColor: 'green',
          borderColor: '#f40'
        }
      },
      data: []
    }
  ],
  visualMap: [
    {
      type: 'piecewise',
      show: true,
      pieces: [
        { min: 10000 },
        { min: 1000, max: 9999 },
        { min: 100, max: 999 },
        { min: 10, max: 99 },
        { min: 1, max: 9 },
        { value: 0 }
      ],
      inRange: {
        color: ['#fff', '#ffaa86', '#660208']
      },
      itemWidth: 10,
      itemHeight: 10
    }
  ],
  tooltip: {
    trigger: 'item',
    formatter: '地区: {b}<br/>确诊: {c}'
  },
  toolbox: {
    show: true,
    orient: 'horizontal',
    left: 'right',
    top: 'top',
    feature: {
      dataView: { readOnly: false },
      restore: {},
      saveAsImage: {}
    }
  }
};

export default {
  name: 'Map',
  data() {
    return {
      myChart: null
    };
  },
  methods: {
    init() {
      this.myChart = echarts.init(document.querySelector('.map-box'));
    },
    getData() {
      jsonp('https://interface.sina.cn/news/wap/fymap2020_data.d.json?_=1580892522427', (err, data) => {
        if (!err) {
          const list = data.data.list.map((item) => ({ name: item.name, value: item.value}));
          option.series[0].data = list;
          this.myChart.setOption(option);
        }
      });
    }
  },
  mounted() {
    this.init();
    this.getData();
  }
};
</script>

<style lang="less" scoped>
.map {
  width: 800px;
  height: 600px;
  margin: 0 auto;

  .map-box {
    width: 100%;
    height: 100%;
    padding: 20px;
    border-radius: 6px;
    box-shadow: 0 0 10px #ccc;
  }
}
</style>
