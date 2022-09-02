<template>
  <div class="visibleDiv">
    <div id="energyPie" :style="{width: '100%', height: '250px'}"></div>
  </div>
</template>
<script type="text/ecmascript-6">
export default {
  name: 'modal',
  data() {
    return {}
  },
  mounted() {
    this.getList()
  },
  created() {
  },
  methods: {
    getList() {
      var data = [
        {"value": '61.17', "name": "煤品"},
        {"value": '27.16', "name": "电力"},
        {"value": '16.48', "name": "热量"},
        {"value": '16.48', "name": "油品"},
        {"value": '0.26', "name": "天然气"},
        {"value": '0.26', "name": "其他"}
      ]
      let colorList = ['#4CE4C3', '#4BD5F5', '#9994DB', '#837DED', '#666666', '#E44CE2','#3240FF']
      let myChart = this.$echarts.init(document.getElementById('energyPie'))
      // 绘制图表
      myChart.setOption({
        tooltip: {
          trigger: 'item'
        },
        title: {
          text: '',
          subtext: '',
          left: 'center'
        },
        legend: {
          top: '85%',
          left: 'center',
        },
        toolbox: {
          show: true,
          feature: {
            mark: { show: true },
            dataView: { show: true, readOnly: false },
            restore: { show: true },
            saveAsImage: { show: true }
          }
        },
        series: [
          {
            name: '',
            type: 'pie',
            radius: ['40%', '70%'],
            avoidLabelOverlap: true,
            itemStyle: {
              normal: {
                color: function(colors) {
                  var colorList = ['#4CE4C3', '#4BD5F5', '#9994DB', '#837DED', '#666666', '#E44CE2','#3240FF'];
                  return colorList[colors.dataIndex]
                },
                label: {
                  show: true,
                  formatter: '{d}%'
                },
                labelLine: { show: true }
              }
            },
            label: {
              show: false,
              position: 'center'
            },
            emphasis: {
              label: {
                show: false,
                fontSize: '40',
                fontWeight: 'bold'
              }
            },
            labelLine: {
              show: false
            },
            data: data
          }
        ]
      });
    }
  },
  props: {}
}
</script>
<style lang="scss" scoped>
.visibleDiv {
  width: 100%;
  height: 330px;
}
</style>
