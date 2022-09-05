<template>
  <div class="visibleDiv">
    <div id="mapDiv" :style="{width: '100%', height: '300px'}"></div>
  </div>
</template>
<script type="text/ecmascript-6">
export default {
  name: 'Modal',
  data() {
    return {}
  },
  mounted() {
    this.$nextTick(() => {
      this.getList()
    })
  },
  created() {
  },
  methods: {
    getList() {
      var data = [
        {
          "name": "历下区", "value": "88", "id": "2"
        },
        {
          "name": "市中区", "value": "69.9", "id": "3"
        },
        {
          "name": "槐荫区", "value": "79", "id": "4"
        },
        {
          "name": "天桥区", "value": "49.9", "id": "1"
        },
        {
          "name": "历城区", "value": "39.9", "id": "5"
        },
        {
          "name": "长清区", "value": "19.9", "id": "6"
        },
        {
          "name": "章丘区", "value": "29.9", "id": "7"
        },

        {
          "name": "济阳区", "value": "29.9", "id": "7"
        },
        {
          "name": "莱芜区", "value": "29.9", "id": "7"
        },
        {
          "name": "钢城区", "value": "29.9", "id": "7"
        },
        {
          "name": "平阴县", "value": "29.9", "id": "7"
        },
        {
          "name": "商河县", "value": "29.9", "id": "7"
        }
      ]
      const arrList = []
      for (let i = 0; i < data.length; i++) {

        let json = {
          "name": data[i].name, "value": data[i].value, "id": data[i].id,"label": {
            normal: {
              show: true,
              formatter: function (params) {
                return params.name + "\n" + params.value;    //地图上展示文字 + 数值
              },
            }
          }
        }
        arrList.push(json)
      }
      var myChart = this.$echarts.init(document.getElementById('mapDiv'))
      myChart.on('click', function(params) {})
      myChart.setOption({
        visualMap: {
          show: true,
          min: 0,
          max: 100,
          text: ['高', '低'],
          realtime: true,
          calculable: true,
          hoverLink: true,
          inRange: {
            color: ['#B3C8E7', '#0449AE']
          },
        },
        geo: {
          map: '山东',
          roam: true,
          aspectScale: 0.75,
          zoom: 1.20,
          label: {
            normal: {
              show: true,
              textStyle: {
                color: '#FFFFFF'
              }
            },
            emphasis: {
              show: false,
              textStyle: {
                color: "#00a0c9"
              }
            }
          },
          itemStyle: {
            normal: {
              areaColor: '#0083ce',
              borderColor: '#0066ba'
            },
            emphasis: {
              borderWidth: 0,
              borderColor: '#0066ba',
              areaColor: "#0494e1",
              shadowColor: 'rgba(0, 0, 0, 0.5)'
            }
          }
        },
        series: [{
          name: '',
          type: 'map',
          map: '山东',
          mapType: '山东',
          roam: true,
          coordinateSystem: 'geo',
          geoIndex: 0,
          aspectScale: 0.75,
          zoom: 1.2,
          label: {
            normal: {
              formatter: '{b}',
              position: 'right',
              show: false
            },
            emphasis: {
              show: true
            }
          },
          itemStyle: {
            normal: {
              color: '#F06C00'
            }
          },
          data: arrList
        }]
      })
      window.addEventListener("resize", function() {
        myChart.resize()
      })
    }
  },
  props: {}
}
</script>
<style lang="scss" scoped>
.visibleDiv {
  width: 100%;
  height: 360px;
}
</style>
