<template>
  <div class="visibleDiv">
    <div id="industryBar" :style="{width: '100%', height: '380px'}"></div>
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
      let myChart1 = this.$echarts.init(document.getElementById('industryBar'))
      // 绘制图表
      myChart1.setOption(
        {
          legend: {
            data:['SO₂', 'NOx', 'PM2.5', 'VOCs'],
            textStyle: {
              fontSize: 12,
              color: '#5D6464'
            }
          },
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'shadow'
            }
          },
          grid: {
            top: '6%',
            left: '3%',
            right: '10%',
            containLabel: true
          },
          /* toolbox: {
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
          },*/
          xAxis: [
            {
              name: "",
              type: 'value',
              data: ['10', '20', '30', '40', '50', '60', '70', '80'],
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
              data: ['钢铁', '炼化', '焦化', '煤电', '肥料', '轮胎', '水泥', '石灰', '玻璃', '陶瓷', '有色', '铸造', '煤加工', '铁合金', '化学原料', '防水建材'],
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
              barWidth: '30%',
              stack: 'jl',
              name:"SO₂",
              data: [11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,22, 23, 24, 25, 26],
              itemStyle: {
                normal: {
                  color: function(params) {
                    var colorList = ['#37A0E4']
                    return colorList[params.dataIndex]
                  },
                  barBorderRadius: [0, 10, 10, 0]
                }
              }
            },
            {
              type: 'bar',
              barWidth: '30%',
              stack: 'jl',
              name:"NOx",
              data: [11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,22, 23, 24, 25, 26],
              itemStyle: {
                normal: {
                  color: function(params) {
                    var colorList = ['#29D078']
                    return colorList[params.dataIndex]
                  },
                  barBorderRadius: [0, 10, 10, 0]
                }
              }
            },
            {
              type: 'bar',
              barWidth: '30%',
              stack: 'jl',
              name:"PM2.5",
              data: [11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,22, 23, 24, 25, 26],
              itemStyle: {
                normal: {
                  color: function(params) {
                    var colorList = ['#4ECEE5']
                    return colorList[params.dataIndex]
                  },
                  barBorderRadius: [0, 10, 10, 0]
                }
              }
            },
            {
              type: 'bar',
              barWidth: '30%',
              stack: 'jl',
              name:"VOCs",
              data: [11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21,22, 23, 24, 25, 26],
              itemStyle: {
                normal: {
                  color: function(params) {
                    var colorList = ['#FBD55A']
                    return colorList[params.dataIndex]
                  },
                  barBorderRadius: [0, 10, 10, 0]
                }
              }
            }
          ]
        }, true)
    }
  },
  props: {}
}
</script>
<style lang="scss" scoped>
.visibleDiv {
  width: 100%;
  height: 380px;
}
</style>
