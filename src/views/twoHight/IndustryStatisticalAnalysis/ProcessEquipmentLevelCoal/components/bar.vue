<template>
  <div class="visibleDiv">
    <div id="Bar" :style="{width: '100%', height: '280px'}"></div>
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
      let myChart1 = this.$echarts.init(document.getElementById('Bar'))
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
              data: ['焦炉', '封顶', '捣固'],
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
              min: '0',
              max: '200',
              axisLabel: {
                textStyle: {
                  color: "#5D6464"
                }
              }
            }
          ],
          series: [
            {
              name: '',
              type: 'bar',
              barWidth: '30%',
              stack: 'jl',
              data: [43, 51, 76],
              label: {
                show: true
              },
              itemStyle: {
                normal: {
                  color: '#41CDE6'
                }
              }
            },
            {
              name: '',
              type: 'bar',
              stack: 'jl',
              barWidth: '30%',
              label: {
                show: true
              },
              data: [65, 21, 32],
              itemStyle: {
                normal: {
                  color: '#3377FF'
                }
              }
            },
            {
              name: '',
              type: 'bar',
              stack: 'jl',
              label: {
                show: true
              },
              barWidth: '30%',
              data: [35, 54, 45],
              itemStyle: {
                normal: {
                  color: '#4CE4C3'
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
