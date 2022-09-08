<template>
  <div class="visibleDiv">
    <div id="mapDiv" :style="{width: '100%', height: '350px'}"></div>
  </div>
</template>
<script type="text/ecmascript-6">
export default {
  name: 'Modal',
  props: {},
  data() {
    return {}
  },
  computed: {},
  watch: {},
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
        },
      ]
      let arr = []
      for (let i = 0; i < data.length; i++) {

        let json = {
          "name": data[i].name, "value": data[i].value, "id": data[i].id, "label": {
            normal: {
              show: true,
              formatter: function (params) {
                return params.name + "\n" + params.value;    //地图上展示文字 + 数值
              },
            }
          }
        }
        arr.push(json)
      }
      var myChart = this.$echarts.init(document.getElementById('mapDiv'))
      myChart.on('click', function (params) {
      })
      myChart.setOption({
        title: {
          text: ''
        },
        tooltip: {
          trigger: 'item',
          formatter: '{b}',
          itemSize: '14px'
        },
        dataRange: {
          x: 'left',
          y: 'center',
          top: '100',
          splitList: [
            {start: 81, end: 100, label: '', color: '#0449AE'},
            {start: 71, end: 80, label: '', color: '#1D5BB6'},
            {start: 51, end: 70, label: '', color: '#356BBA'},
            {start: 41, end: 50, label: '', color: '#1D5BB6'},
            {start: 31, end: 40, label: '', color: '#366DBE'},
            {start: 21, end: 30, label: '', color: '#4F7EC5'},
            {start: 0, end: 20, label: '', color: '#4671B0'},
          ],
          textStyle: {
            color: '#3899FF' // 值域文字颜色
          },
          show: false,
          selectedMode: false,
          color: ['#E0022B', '#E09107', '#A3E00B']
        },
        series: [
          {
            name: '县域乡村振兴全景展示',
            type: 'map',
            map: '山东',
            mapType: '山东',
            mapLocation: {
              x: 'left'
            },
            zoom: 1.2,
            roam: true,
            show: true,
            itemStyle: {
              normal: {
                borderColor: "#fff",
                type: 'dashed',
                borderWidth: 1,
                label: {show: true}
              },
              emphasis: {
                areaColor: '#389BB7',
                borderWidth: 0
              }
            },
            label: {
              normal: {
                show: true,
                formatter: function (params) { //标签内容
                  return params.name;
                },
                lineHeight: 12,
                backgroundColor: '#FFFFFF',
                borderColor: '#80cffd',
                borderWidth: '1',
                padding: [5, 15, 5],
                color: '#000000',
                fontSize: 14,
                fontWeight: 'normal',
              },
              emphasis: {
                show: true,
                textStyle: {
                  color: '#000000',
                }
              },
            },
            showEffectOn: 'render',
            rippleEffect: {
              brushType: 'stroke'
            },
            hoverAnimation: true,
            data: arr
          }],
      })
      window.addEventListener("resize", function () {
        myChart.resize()
      })
    }
  }
}
</script>
<style lang="scss" scoped>
.visibleDiv {
  width: 100%;
  height: 360px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
