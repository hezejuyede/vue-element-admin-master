<template>
  <div class="visibleDiv">
    <div id="regionBar" :style="{width: '100%', height: '350px'}"></div>
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
      let myChart1 = this.$echarts.init(document.getElementById('regionBar'))
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
            top: '2%',
            left: '3%',
            right: '10%',
            containLabel: true
          },
          /*   toolbox: {
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
              data: ['10', '20', '30', '40', '50', '60', '70', '80'],
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
              data:  ['济南市', '青岛市', '淄博市', '枣庄市', '东营市', '烟台市', '潍坊市', '济宁市', '泰安市', '威海市', '日照市', '临沂市', '德州市', '聊城市', '滨州市', '菏泽市'],
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
  height: 330px;
}
</style>
