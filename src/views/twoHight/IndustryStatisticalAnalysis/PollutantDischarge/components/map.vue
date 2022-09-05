<template>
  <div class="visibleDiv">
    <div id="mapDiv" :style="{width: '100%', height: '330px'}"></div>
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
          show: false,
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
              show: true,
              textStyle: {
                color: "#FFFFFF"
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
        title: {
          name: '污染物排放量',
          top: "1%",
          left: "center",
          textStyle: {
            fontSize: 20,
            fontWeight: 600,
            color: "#222",
          },
        },
        tooltip: {
          trigger: 'item',
          triggerOn: "mousemove",
          showContent: true,
          alwaysShowContent: true,
          showDelay: 0,
          hideDelay: 100,
          enterable: false,
          confine: false,
          transitionDuration: 0.4,
          position: ['2%', '2%'],
          formatter: function(params) {
            const showname = params
            return (
              `
                <div style='width:150px;height:120px;background-color: #ffffff'>
                    <p  style="width:100%;height:15px;text-align: center;line-height: 15px;font-size: 14px">${showname.data.name}污染物排放量</p>
                    <p  style="width:100%;height:10px;line-height: 10px;text-align: center">
                    <span>SO₂:</span><span style="color: #3B7BFF;font-size: 14px;margin-left: 5px">${showname.data.value}[吨]</span>
                    </p>
                    <p  style="width:100%;height:10px;line-height: 10px;text-align: center">
                    <span>NOx:</span><span style="color: #3B7BFF;font-size: 14px;margin-left: 5px">${showname.data.value}[吨]</span>
                    </p>
                    <p  style="width:100%;height:10px;line-height: 10px;text-align: center">
                    <span>PM2.5:</span><span style="color: #3B7BFF;font-size: 14px;margin-left: 5px"> ${showname.data.value}[吨]</span>
                    </p>
                    <p  style="width:100%;height:10px;line-height: 10px;text-align: center">
                    <span>VOCs:</span><span style="color: #3B7BFF;font-size: 14px;margin-left: 5px">${showname.data.value}[吨]</span>
                    </p>
              </div>
              `
            )
          },
          backgroundColor: "transparent",
          borderColor: "#ccc",
          borderWidth: 1,
          padding: 0,
          textStyle: '',
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
          label: {},
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
