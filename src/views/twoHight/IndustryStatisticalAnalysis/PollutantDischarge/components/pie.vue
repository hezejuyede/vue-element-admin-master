<template>
  <div class="visibleDiv">
    <div class="visibleDivL">
      <div id="pie" :style="{width: '100%', height: '360px'}"></div>
    </div>
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
    this.getList2()
  },
  created() {
  },
  methods: {
    getList1() {
      var data = [
        {"name": "历下区", "value": "88", "id": "2"},
        {"name": "市中区", "value": "69.9", "id": "3"},
        {"name": "槐荫区", "value": "79", "id": "4"},
        {"name": "天桥区", "value": "49.9", "id": "1"},
        {"name": "历城区", "value": "39.9", "id": "5"},
        {"name": "长清区", "value": "19.9", "id": "6"},
        {"name": "章丘区", "value": "29.9", "id": "7"},
        {"name": "济阳区", "value": "29.9", "id": "7"},
        {"name": "莱芜区", "value": "29.9", "id": "7"},
        {"name": "钢城区", "value": "29.9", "id": "7"},
        {"name": "平阴县", "value": "29.9", "id": "7"},
        {"name": "商河县", "value": "29.9", "id": "7"}
      ]
      let colorList = ['#4CE4C3', '#4BD5F5', '#9994DB', '#837DED', '#666666', '#E44CE2', '#3240FF']
      let myChart = this.$echarts.init(document.getElementById('pie'))
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
          top: '87%',
          left: 'center',
        },
        toolbox: {
          show: true,
          feature: {
            mark: {show: true},
            dataView: {show: true, readOnly: false},
            restore: {show: true},
            saveAsImage: {show: true}
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
                color: function (colors) {
                  var colorList = ['#4CE4C3', '#4BD5F5', '#9994DB', '#837DED', '#666666', '#E44CE2', '#3240FF'];
                  return colorList[colors.dataIndex]
                },
                label: {
                  show: true,
                  formatter: '{d}%'
                },
                labelLine: {show: true}
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
      })
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
