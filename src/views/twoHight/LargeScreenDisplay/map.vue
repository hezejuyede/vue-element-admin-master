<template>
  <div>
    <ul>
      <li v-for="(value,k) of addres" :key="k" @click="map(value)">{{ k }}</li>
    </ul>
    <div id="County" :style="{width: '100%', height: '470px'}"></div>
  </div>

</template>
<script>
import axios from 'axios'
import echarts from 'echarts'

export default {
  data() {
    return {
      code: 370200, //370100济南
      addres: {
        济南市: "370100",
        青岛市: "370200",
        淄博市: "370300",
        枣庄市: "370400",
        东营市: "370500",
        烟台市: "370600",
        潍坊市: "370700",
        济宁市: "370800",
        泰安市: "370900",
        威海市: "371000",
        日照市: "371100",
        莱芜市: "371200",
        临沂市: "371300",
        德州市: "371400",
        聊城市: "371500",
        滨州市: "371600",
        菏泽市: "371700",
      }
    }
  },
  mounted() {
  },
  methods: {
    map(code) {
      //我这里直接获取static文件夹中的json文件，this.code是点击全省发送过来的城市对应的行政代码
      //也可以写'https://geo.datav.aliyun.com/areas_v2/bound'+this.code+'_full.json'
      axios.get('https://geo.datav.aliyun.com/areas_v3/bound/' + code + '_full.json').then(response => {
        echarts.registerMap('county', response.data)
        var chart = echarts.init(document.getElementById("County"));
        chart.setOption({
          backgroundColor: '#142942', //地图背景颜色
          title: {},
          legend: {},
          tooltip: {
            appendToBody: true,
            triggerOn: 'click',   //触发方式
            enterable: true, //
            trigger: 'item',
            confine: true,
            alwaysShowContent: false,
            formatter: function (params) {//点击进入下级城市的点击事件可以写在这个div里
              return `
                                <div class='pop-up'>
                                    <div class='pop-up-title'>
                                        <p style="margin:0;">地区：` + params.name + `</p>
                                        <p style="margin:0;">人数：` + params.value + `</p>
                                    </div>&nbsp;&nbsp;&nbsp;&nbsp;
                                </div>`
            },
          },
          visualMap: {
            type: 'piecewise',
            orient: 'horizontal',
            realtime: false,
            left: '5%',
            bootom: 'bootom',
            textStyle: {
              color: "rgba(232, 218, 218, 1)"
            },
            pieces: [
              {min: 10, max: 25, label: '点亮数11—25'},
              {min: 1, max: 10, label: '点亮数1—10'},
              {max: 1, label: '未点亮区域'}
            ],
            color: ['#5adf5a', '#c4ffc4', '#4a5b71'],
          },
          geo: { // 这个是重点配置区
            map: 'county', // 需要对应echarts.registerMap('county',response.data)
            roam: true,
            zoom: 1.2,
            label: {
              normal: {
                show: false, // 是否显示对应地名，
                textStyle: {
                  color: '#b7cfee'
                }
              },
              emphasis: {
                show: true,
                textStyle: {
                  color: '#cc3041'
                }
              }
            },
            itemStyle: {
              normal: {//地图背景色
              },
            }
          },
          series: [{
            type: 'scatter',
            coordinateSystem: 'geo' // 对应上方配置
          }, {
            type: 'map',
            zoom: 1.25,
            mapType: 'county',
            geoIndex: 0,
            roam: false,
            showLegendSymbol: true,
            data: [
              //这里写获取到的后台数据，或者你自己需要加载的数据
            ]
          }]
        });
        return chart
      }, response => {
        console.log('失败');
      });
    }
  }
}
</script>
<style lang="scss">
ul {
  display: flex;

  li {
    margin: 10px;
    padding: 0 10px;
  }
}
</style>
