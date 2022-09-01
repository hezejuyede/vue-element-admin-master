<template>
  <div class="visibleDiv">
    <div id="enterpriseBar" :style="{width: '100%', height: '400px'}"></div>
  </div>
</template>
<script type="text/ecmascript-6">
import Chart from '@/components/Charts/LineMarker'
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

      let myChart1 = this.$echarts.init(document.getElementById('enterpriseBar'));
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
            right:'center',
            top:0,
            feature: {
              mark: { show: true },
              magicType: { show: true, type: ['line', 'bar'] },
              restore: { show: true },
              saveAsImage: { show: true },
              dataView: { show: true },
              dataZoom: { show: true }
            }
          },
          xAxis: [
            {
              type: 'category',
              data:  ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
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
              name: "万元",
              axisLine: {
                show: false
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
              data: [190, 352, 200, 334, 390, 330, 220,430, 252, 200, 334, 390],
              smooth: true, symbol: 'circle', symbolSize: 10, itemStyle: {normal: {
                  color: '#3979FA', areaStyle: {
                    type: 'default',
                    opacity: 0.1
                  }
                }
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
  height: 400px;
}
</style>
