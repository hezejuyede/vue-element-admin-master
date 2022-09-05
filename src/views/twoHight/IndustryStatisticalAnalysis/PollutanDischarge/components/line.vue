<template>
  <div class="visibleDiv">
    <div id="productLine" :style="{width: '100%', height: '200px'}"></div>
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
      let myChart1 = this.$echarts.init(document.getElementById('productLine'))
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
            right: '4%',
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
              data: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'],
              type: 'category',
              axisLine: {
                lineStyle: {
                  color: "#3A4467"
                }
              },
              offset: 10,
              axisTick: { //x轴刻度线
                show: false,
              },
              splitLine: {show: false},
              axisLabel: {
                rotate: 30,
                textStyle: {
                  color: "#5D6464"
                }
              },
            }
          ],
          yAxis: [
            {
              name: "t",
              axisLine: {
                show: false,
              },
              axisTick: { //y轴刻度线
                show: false,
                axisLine: { //y轴
                  show: false
                },

              },
              splitLine: {
                lineStyle: {
                  color: "#EDEDED"
                }
              },
              axisLabel: {
                textStyle: {
                  color: "#5D6464"
                }
              }
            }
          ],
          series: [
            {
              name: 'Direct',
              type: 'line',
              data: [200, 334, 390, 330, 220, 200, 334, 390, 330, 220, 200, 334, 200, 334, 390, 330, 220, 200, 334, 390, 330, 220, 200, 390],
              symbol: 'circle', symbolSize: 10, smooth: true, itemStyle: { normal: { color: '#4180FF' }
              }
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
