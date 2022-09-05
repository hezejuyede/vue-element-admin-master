<template>
  <div class="visibleDiv">
    <div id="line" :style="{width: '100%', height: '400px'}"></div>
  </div>
</template>
<script type="text/ecmascript-6">
export default {
  name: 'modal',
  data() {
    return {}
  },
  mounted() {
    this.getList1()
  },
  created() {
  },
  methods: {
    getList1() {
      const data = [
        ['单元', 'SO₂', 'NOx', 'PM2.5', 'VOCs'],
        ['1', 494.12, 595.47, 795.47, 895.47],
        ['2', 461.18, 562.44, 795.47, 895.47],
        ['3', 433.95, 635.13, 795.47, 895.47],
        ['4', 414.95, 716.08, 795.47, 595.47],
        ['5', 403.64, 804.74, 795.47, 895.47],
        ['6', 458.21, 959.47, 795.47, 895.47],
        ['7', 469.41, 270.70, 795.47, 895.47],
        ['8', 516.96, 318.37, 795.47, 895.47],
        ['9', 501.26, 802.63, 795.47, 895.47],
        ['10', 488.08, 789.41, 795.47, 895.47],
        ['11', 483.91, 685.23, 795.47, 895.47],
        ['12', 535.84, 137.31, 795.47, 895.47]
      ];
      let myChart = this.$echarts.init(document.getElementById('line'));

      // 绘制图表
      myChart.setOption(
        {
          legend: {
            textStyle: {
              fontSize: 12,//字体大小
              color: '#5D6464'//字体颜色
            },
          },
          tooltip: {
            trigger: 'item',
            textStyle: {
              color: '#FFFFFF'
            },
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          dataset: {
            source: data
          },
          xAxis: {
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
              rotate: 0,
              textStyle: {
                color: "#5D6464"
              }
            },
          },
          yAxis: {
            name: "mg/m³",
            axisLine: {
              show: true,
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
          },
          series: [{
            type: 'line', smooth: true, itemStyle: {
              normal: {
                color: '#088B86', areaStyle: {
                  type: 'default',
                  opacity: 0.1
                }
              }
            }
          },
            {
              type: 'line', smooth: true, itemStyle: {
                normal: {
                  color: '#FFC657', areaStyle: {
                    type: 'default',
                    opacity: 0.1
                  }
                }
              }
            },
            {
              type: 'line', smooth: true, itemStyle: {
                normal: {
                  color: '#78D44B', areaStyle: {
                    type: 'default',
                    opacity: 0.1
                  }
                }
              }
            },
            {
              type: 'line', smooth: true, itemStyle: {
                normal: {
                  color: '#0EA3F7', areaStyle: {
                    type: 'default',
                    opacity: 0.1
                  }
                }
              }
            }]
        }, true);
    },
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
