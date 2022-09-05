<template>
  <div class="visibleDiv">
    <div id="energyBar" :style="{width: '100%', height: '200px'}"></div>
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
      let myChart2 = this.$echarts.init(document.getElementById('energyBar'));
      // 绘制图表
      myChart2.setOption(
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
              axisTick: {
                show: false,
                axisLine: {
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
              type: 'bar',
              barWidth: '30%',
              data: [300, 334, 390, 330, 220,200, 334, 390, 330, 220, 200, 334],
              itemStyle: {
                normal: {
                  color: '#32A4BF',
                  barBorderRadius:[10, 10, 0, 0]
                }
              }}]
        }, true)

      window.onresize = myChart2.resize
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
