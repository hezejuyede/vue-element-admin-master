<template>
  <div class="visibleDiv">
    <div id="industryBar" :style="{width: '100%', height: '350px'}"></div>
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
      let myChart1 = this.$echarts.init(document.getElementById('industryBar'));
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
              mark: { show: true},
              magicType: { show: true, type: ['line', 'bar'] },
              restore: { show: true },
              saveAsImage: { show: true },
              dataView: { show: true },
              dataZoom: { show: true }
            }
          },
          xAxis: [
            {
              data: ['汽油', '煤油', '柴油', '石脑油', '溶剂油', '燃料油', '石油', '沥青', '乙烯', 'PX', '液化气', '其他'],
              type: 'category',
              axisLine: {
                lineStyle: {
                  color: "#3A4467"
                }
              },
              offset: 10,
              axisTick: {
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
              type: 'bar',
              barWidth: '30%',
              data: [200, 334, 390, 330, 220, 200, 334, 390, 330, 220, 334, 252],
              itemStyle: {
                normal: {
                  color: '#32A4BF',
                  barBorderRadius: [10, 10, 0, 0]
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
  height: 330px;
}
</style>
