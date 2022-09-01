<template>
  <div class="visibleDiv">
    <div id="trendBar" :style="{width: '100%', height: '290px'}"></div>
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
      let myChart1 = this.$echarts.init(document.getElementById('trendBar'))
      // 绘制图表
      myChart1.setOption(
        {
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'shadow'
            }
          },
          grid: {
            left: '3%',
            right: '10%',
            bottom: '3%',
            containLabel: true
          },
          toolbox: {
            show: true,
            right: 'center',
            top: 0,
            feature: {
              mark: {show: true},
              magicType: {show: true, type: ['line', 'bar']},
              restore: {show: true},
              saveAsImage: {show: true},
              dataView: {show: true},
              dataZoom: {show: true}
            }
          },
          xAxis: [
            {
              name: "万元",
              type: 'value',
              splitLine: {
                lineStyle: {
                  color: "#EDEDED"
                }
              },
              axisTick: {
                show: false,
                axisLine: {
                  show: false
                }
              }
            }
          ],
          yAxis: [
            {
              type: 'category',
              data: ['入库税', '利润', '主业营收', '产值'],
              axisLine: {
                show: true
              },
              axisTick: { //y轴刻度线
                show: false,
                axisLine: { //y轴
                  show: false
                }
              },
            }
          ],
          series: [
            {
              type: 'bar',
              showBackground: true,
              barWidth: '30%',
              data: [10, 52, 200, 334],
              itemStyle: [
                {
                  normal: {
                    color: function(params) {
                      var colorList = ['#B259EE', '#FFD035', '#3377FF', '#00CC60'];
                      return colorList[params.dataIndex]
                    },
                    barBorderRadius: [10, 10, 0, 0]
                  }
                }
              ]
            }]
        }, true)
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
