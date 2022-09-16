<template>
    <ScaleBox>
        <div class="templateDiv">
            <!--header-->
            <div class="header"></div>
            <!--main-->
            <div class="main">
                <!-- 信息 -->
                <div class="message">
                    <!-- 面包屑 -->
                    <div class="crumbs">
                        <div>当前位置:</div>
                        <span>首页</span>
                        <div>> 项目汇总分析</div>
                    </div>
                    <!-- 时间 -->
                    <date class="time">2022年8月11 星期四</date>
                </div>
                <!-- 左边 -->
                <div class="left">
                    <!-- 当年能源消费 -->
                    <div class="energy">
                        <div class="title"></div>
                        <!-- 综合 -->
                        <div class="synthesize">
                            <img src="./images/tj_03.png" alt="">
                            <div class="nmb">
                                <span>2986.65</span>
                                <p>综合能耗（万吨标准煤）</p>
                                <p>
                                    <span class="mini">同比上升 </span>
                                    <img src="./images/sh.png" alt="">
                                </p>
                            </div>
                        </div>
                        <!-- 分支 -->
                        <ul class="branch">
                            <li v-for="(item,index) of energy" :key="index">
                                <img :src="require(`./images/tj_${item.img}.png`)" alt="">
                                <div class="nmb">
                                    <span>15952</span>
                                    <p>{{item.name}}</p>
                                    <p>
                                        <span class="mini">同比上升 </span>
                                        <i></i>
                                    </p>
                                </div>
                            </li>
                        </ul>
                    </div>
                    <!-- 区域单位产值能耗 -->
                    <div class="unitOutput">
                        <div class="title"></div>
                        <div id="chart_1" class="chart" style="width:100%;height: 500px"></div>
                    </div>
                </div>
                <!-- 中间 -->
                <div class="center">
                    <!-- 顶部 -->
                    <div class="top">
                        <img src="./images/zong.png" alt="">
                        <ul>
                            <li v-for="(item,index) of synthesize" :key="index">
                                <div class="text">
                                    <i></i>
                                    <span> {{item.name}}</span>
                                </div>
                                <div class="number">
                                    <span>2986</span>
                                    <p>个</p>
                                    <img :src="require(`./images/qux${item.img}.png`)" alt="">
                                </div>
                            </li>
                        </ul>
                    </div>
                    <!-- 地图 -->
                    <div id="mapDiv" :style="{width: '100%', height: '620px'}"></div>
                    <!-- 排行 -->
                    <div class="ranking">
                        <!-- 区域能源消费排行 -->
                        <div class="area rankingList">
                            <div class="title"></div>
                            <table border rules=rows cellspacing=0 align=right frame=void style="width:100%">
                                <tr style="border-bottom: 1px solid rgba(0, 143, 253,.4);">
                                    <th style="width:30%; padding-left: 17px;">名次</th>
                                    <th style="width:30%">区划</th>
                                    <th style="width:40%; padding-right: 33px;">消费数据(万tce)</th>
                                </tr>
                                <tr v-for="(item,index) of areaRanking" :key="index"
                                    style="border-bottom: 1px solid rgba(0, 145, 255,.2);">
                                    <td style="padding-left: 20px;">
                                        <img :src="require(`./images/paim_${item.img}.png`)" alt="">
                                    </td>
                                    <td>{{item.name}}</td>
                                    <td style="padding-right: 20px;">1317.58</td>
                                </tr>
                            </table>
                        </div>
                        <!-- 行业能源消费排行 -->
                        <div class="trade rankingList">
                            <div class="title"></div>
                            <table border rules=rows cellspacing=0 align=right frame=void style="width:100%">
                                <tr style="border-bottom: 1px solid rgba(0, 143, 253,.4);">
                                    <th style="width:30%; padding-left: 17px;">名次</th>
                                    <th style="width:30%">区划</th>
                                    <th style="width:40%; padding-right: 33px;">消费数据(万tce)</th>
                                </tr>
                                <tr v-for="(item,index) of tradeRanking" :key="index"
                                    style="border-bottom: 1px solid rgba(0, 145, 255,.2);">
                                    <td style="padding-left: 20px;">
                                        <img :src="require(`./images/paim_${item.img}.png`)" alt="">
                                    </td>
                                    <td>{{item.name}}</td>
                                    <td style="padding-right: 20px;">1317.58</td>
                                </tr>
                            </table>
                        </div>
                    </div>
                </div>
                <!-- 右边 -->
                <div class="right">
                    <!-- 能源消费结构 -->
                    <div class="structure">
                        <div class="title"></div>
                        <div id="chart_2" class="chart" style="width:100%;height: 312px"></div>
                    </div>
                    <!-- 行业单位产值能耗 -->
                    <div class="industry">
                        <div class="title"></div>
                        <div id="chart_3" class="chart" style="width:100%;height: 500px"></div>
                    </div>
                </div>
            </div>
        </div>
    </ScaleBox>
</template>
<script>
import echarts from 'echarts'
// import Vue from 'vue'
// 自适应
import ScaleBox from './scaleBox/index.vue'
import date from './date.vue'
import shandong from '../../mapList/shandong'
import binzhou from '../../mapList/binzhou'
import dongying from '../../mapList/dongying'
import linyi from '../../mapList/linyi'
import jinan from '../../mapList/jinan'
import dezhou from '../../mapList/dezhou'
import heze from '../../mapList/heze'
import jining from '../../mapList/jining'
import qingdao from '../../mapList/qingdao'
import rizhao from '../../mapList/rizhao'
import zaozhuang from '../../mapList/zaozhuang'
import yantai from '../../mapList/yantai'
import weifang from '../../mapList/weifang'
import zibo from '../../mapList/zibo'
import liaocheng from '../../mapList/liaocheng'
import weihai from '../../mapList/weihai'
import taian from '../../mapList/taian'


export default {
  name: 'index',
  data() {
    return {
      // 能源消费
      energy: [
        {name: '电力(亿千瓦时)', img: "07"},
        {name: '天然气(亿立方米)', img: "10"},
        {name: '煤品(万吨)', img: "14"},
        {name: '油品(万吨)', img: "15"},
        {name: '热量(百万千焦)', img: "18"},
        {name: '其他(亿立方米)', img: "19"},
      ],
      // 中间顶部综合
      synthesize: [
        {name: '存量', img: ""},
        {name: '在建', img: "-e"},
        {name: '拟建', img: "-r"},
        {name: '关停', img: "-t"},
      ],
      // 区域排行
      areaRanking: [
        {name: '青岛市', img: "03"},
        {name: '威海市', img: "06"},
        {name: '滨州市', img: "08"},
        {name: '枣庄市', img: "10"},
      ],
      // 行业排行
      tradeRanking: [
        {name: '煤电', img: "03"},
        {name: '焦化', img: "06"},
        {name: '炼化', img: "08"},
        {name: '钢铁', img: "10"},
      ],

    }
  },
  computed: {},
  components: {ScaleBox, date},
  mounted() {
    this.doSearch();
    this.$nextTick(() => {
      this.getList()
    })
  },
  created() {
  },
  methods: {
    //页面初始
    doSearch() {
      this.regionalEnergy();
      this.energyUse();
      this.industryUse();
      const date = new Date().toLocaleString()
      console.log(date);
    },
    // 区域单位产值能耗 左下柱状
    regionalEnergy() {
      var chartDom = document.getElementById('chart_1');
      var myChart = echarts.init(chartDom);
      var option = {
        color: ["#17A8FF"],
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        // 图表的大小
        grid: {
          left: '0%',
          right: '0%',
          top: '0%',
          bottom: '0%',
          containLabel: true
        },
        legend: {
          show: false
        },
        // 距离外面尺寸
        grid: {
          top: '3%',
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'value',
          boundaryGap: [0, 0.01],
          // 修改刻度标签 相关样式
          axisLabel: {
            color: "rgba(255,255,255,.6)",
            fontSize: "12",
          },
          // x 轴分隔线样式
          splitLine: {
            lineStyle: {
              type: 'dashed',
              color: "rgba(63, 218, 242,0.2)"
            }
          },
          // 设置轴线
          axisLine: {
            lineStyle: {
              color: "rgba(63,218,242,0.5)",
              width: 1,
              type: "solid"
            }
          },
          // 不显示刻度
          axisTick: {
            show: false
          },
          // 刻度范围间隔
          min: 0.50,
          max: 1.0,
        },
        yAxis: {
          type: 'category',//横向
          data: ['菏泽市', '临沂市', '聊城市', '德州市', '滨州市', '日照市', '威海市', '泰安市', '济宁市', '潍坊市', '烟台市', '东营市', '枣庄市', '淄博市', '青岛市', '济南市'],
          // 修改刻度标签 相关样式
          axisLabel: {
            color: "rgba(255,255,255,.6)",
            fontSize: "16"
          },
          // 设置轴线
          axisLine: {
            lineStyle: {
              color: "rgba(63,218,242,0.5)",
              width: 1,
              type: "solid"
            }
          },
          // 不显示刻度
          axisTick: {
            show: false
          },
        },
        series: [
          {
            type: 'bar',
            barWidth: 10,//柱图宽度
            data: [0.838, 0.86, 0.83, 0.84, 0.82, 0.76, 0.78, 0.91, 0.85, 0.92, 0.85, 0.82, 0.92, 0.78, 0.80, 0.79],
            // 渐变色
            itemStyle: {
              normal: {
                color: new echarts.graphic.LinearGradient(
                  0, 0, 1, 0,
                  [
                    {offset: 0, color: '#18FDFE'},
                    {offset: 1, color: '#17A8FF'}
                  ]
                ),
                label: {
                  show: true,		//开启显示
                  position: 'right',	//在右方显示
                  textStyle: {//数值样式
                    color: '#75D1FF'
                  }
                },
              },
            }

          },
        ],
      };
      option && myChart.setOption(option);

    },
    // 能源消耗结构 右上饼图
    energyUse() {
      var chartDom = document.getElementById('chart_2');
      var myChart = echarts.init(chartDom);
      var option = {
        color: [
          "#0263FF",
          "#00BAFF",
          "#FFFFFF",
          "#6E56D2",
          "#9AD119",
          "#49B09F",
        ],
        tooltip: {
          trigger: 'item'
        },
        legend: {
          //图例垂直排列
          orient: 'vertical',
          bottom: '30%',
          left: '60%',
          // 小图标的宽度和高度
          itemWidth: 10,
          itemHeight: 10,
          // 图例圆形
          icon: 'circle',
          symbolKeepAspect: false,
          data: ["电力", "煤品", "热量", "天然气", "油品", "其他"],
          // 修改图例组件的文字为 12px
          textStyle: {
            color: "rgba(255,255,255,.5)",
            fontSize: "16",
          },
          formatter: function (name) {
            let data = option.series[0].data
            // console.log(data, 'data')
            let total = 0
            let tarValue
            for (let i = 0; i < data.length; i++) {
              total += data[i].value
              if (data[i].name == name) {
                tarValue = data[i].value
              }
            }
            //计算出百分比
            let p = ((tarValue / total) * 100).toFixed(2) + '%'
            return `${name}  ${p}`
            //name是名称，v是数值
          },
        },
        series: [
          {
            name: '能源消费',
            type: 'pie',
            // 设置饼形图在容器中的位置
            center: ["30%", "50%"],
            //  修改内圆半径和外圆半径为  百分比是相对于容器宽度来说的
            radius: ["40%", "70%"],
            avoidLabelOverlap: false,
            label: {
              // 不显示标签文字
              show: false,
              position: 'center',
              // formatter: '{d}%',//模板变量有 {a}、{b}、{c}、{d}，分别表示系列名，数据名，数据值，百分比。{d}数据会根据value值计算百分比
            },
            labelLine: {
              // 不显示连接线
              show: false
            },
            data: [
              {value: 27.16, name: "电力"},
              {value: 81.17, name: "煤品"},
              {value: 0.33, name: "热量"},
              {value: 0.26, name: "天然气"},
              {value: 16.48, name: "油品"},
              {value: 0, name: "其他"},
            ],
          }
        ]
      };

      option && myChart.setOption(option);
    },
    // 行业单位产值能耗 右下柱状
    industryUse() {
      var chartDom = document.getElementById('chart_3');
      var myChart = echarts.init(chartDom);
      var option = {
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          },
          // 鼠标移入条形图提示层文字的自定义
          formatter(params) {
            let relVal = params[0].name
            for (var i = 0, l = params.length; i < l; i++) {
              // console.log(params)
              let circle = `<i class="iconfont icon-yuan" style="margin-right:4px;font-size:14px;color:${params[i].color}"></i>`
              params[i].value = Math.abs(params[i].value)
              relVal += '<br/>' + circle + params[i].seriesName + ' : ' + params[i].value + 'ms'
            }
            return relVal
          }
        },
        legend: {
          data: ['本月', '上月'],
          top: '3%',
          left: "40%",
          textStyle: {
            color: "rgba(255,255,255,.5)",
            fontSize: "16",
          },
        },
        grid: {
          left: '-10%',
          right: '0%',
          bottom: '0%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'value',
            // 设置x轴线的属性
            splitLine: {
              show: false//不显示分隔线
            },
            axisLine: {
              show: false, //不显示坐标轴线,
              lineStyle: {
                color: '#888'
              }
            },
            axisLabel: {
              show: false, //不显示坐标轴上的文字
              formatter(value) {
                return Math.abs(value) // 负数取绝对值变正数（x轴本来数据是正负才能分开两边展示的，所以我们只是把负数处理为正数在视觉上显示）
              }
            }
          }
        ],
        yAxis: [
          {
            type: 'category',
            axisTick: {show: false},
            // 修改刻度标签 相关样式
            axisLabel: {
              // interval: 0,//横轴信息全部显示
              margin: 65,//刻度标签与轴线之间的距离。
              color: "rgba(255,255,255,.6)",
              fontSize: "16",
              textStyle: {
                align: 'left'
              }
            },
            // 设置y轴线的属性
            axisLine: {
              show: false, //不显示坐标轴线
            },
            data: ['铸造', '轮胎', '煤加工', '煤电', '钢铁', '炼化', '焦化', '石灰', '水泥', '化学原料', '房复', '陶瓷', '玻璃', '铁合金', '有色', '防水建材', '肥料'] // y轴下到上
          }
        ],
        color: ['#98d87d', '#49a9ee'],
        series: [
          {
            name: '上月',
            type: 'bar',
            stack: '总量',
            barMaxWidth: '22',
            barWidth: '45%',//柱图宽度
            // barGap: '-100%',
            // barCategoryGap: '10',
            label: {
              normal: {
                show: true,
                color: '#444',
                align: 'left',
              }
            },
            // 渐变色
            itemStyle: {
              barBorderRadius: 5,
              normal: {
                color: new echarts.graphic.LinearGradient(
                  0, 0, 1, 0,
                  [
                    {offset: 0, color: '#38F5CE'},
                    {offset: 1, color: '#44EA84'}
                  ]
                ),
                label: {
                  show: true,		//开启显示
                  position: 'right',	//在右方显示
                  textStyle: {//数值样式
                    color: 'rgba(56, 244, 205,.5)'
                  }
                },
                //柱形图圆角，初始化效果
                barBorderRadius: 10,
              }
            },
            data: [
              103.85, 93.85, 86.26, 76.26, 66.26, 54.21, 50.26, 46.78, 43.45, 36.26, 35.26, 34.26, 32.26, 25.23, 15.26, 15.26, 8.26
            ]
          },
          {
            name: '本月',
            type: 'bar',
            stack: '总量', // 数据堆叠，同个类目轴上系列配置相同的stack值可以堆叠放置。
            barMaxWidth: '22',
            barWidth: '45%',//柱图宽度
            // 渐变色
            itemStyle: {
              barBorderRadius: 5,
              normal: {
                color: new echarts.graphic.LinearGradient(
                  0, 0, 1, 0,
                  [
                    {offset: 0, color: '#00BAFF'},
                    {offset: 1, color: '#0263FF'}
                  ]
                ),
                label: {
                  show: true,		//开启显示
                  position: 'left',	//在右方显示
                  textStyle: {//数值样式
                    color: 'rgba(0, 186, 255,.5)'
                  }
                },
                //柱形图圆角，初始化效果
                barBorderRadius: 10,
              }
            },
            label: {
              normal: {
                show: true,
                color: '#444',
                align: 'right',
                formatter(params) {
                  let htmlStr = Math.abs(params.value)
                  return htmlStr
                }
              }
            },
            data: [-103.85, -93.85, -86.26, -76.26, -66.26, -54.21, -50.26, -46.78, -43.45, -36.26, -35.26, -34.26, -32.26, -25.23, -15.26, -15.26, -8.26]
          }
        ]
      }
      option && myChart.setOption(option);
    },
    // 地图
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

      echarts.registerMap('china',taian)
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
          itemSize: '14px',
          lineHeight: 12,
          backgroundColor: 'rgb(7, 28, 56)',
          borderWidth: '1',
          padding: [3, 2, 2, 9],
          color: '#fff',
          fontSize: 14,
          fontWeight: '400',
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
                areaColor: "rgba(10,126,217, 0.8)",
                borderColor: "#04B4F3",
                type: 'dashed',
                borderWidth: 2,
                label: {show: true}
              },
              emphasis: {
                areaColor: '#E85706',
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
                backgroundColor: 'rgb(7, 28, 56)',
                borderWidth: '1',
                padding: [3, 2, 2, 9],
                color: '#fff',
                fontSize: 14,
                fontWeight: '400',
              },
              emphasis: {
                show: true,
                textStyle: {
                  color: '#fff',
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
<style lang="scss">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.templateDiv {
    position: relative;
    background: url(./images/bg.png) no-repeat;
    background-size: 100% 100%;
    width: 1920px;
    height: 1080px;
}

.header {
    width: 1920px;
    height: 85px;
    background: url(./images/daping_01.png) no-repeat;
    background-size: 100% 100%;
}

.main {
    margin: 25px 21px 0;

    .message {
        width: 100%;
        display: flex;
        justify-content: space-between;
        margin-bottom: 33px;

        .crumbs {
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 254px;
            height: 16px;
            font-size: 16px;
            font-family: SourceHanSansCN;
            font-weight: 400;
            color: #FFFFFF;
            line-height: 11px;
            // margin: 25px 0 30px 21px;

            span {
                color: #3ED7EE;
            }
        }

        .time {
            width: 180px;
            height: 16px;
            font-size: 16px;
            font-family: SourceHanSansCN;
            font-weight: 400;
            color: #FFFFFF;
            line-height: 11px;
            text-align: right;
        }
    }

    .left {
        display: inline-block;
        overflow: hidden;

        .energy {
            width: 436px;
            height: 350px;
            border-top: 2px solid #09375D;
            background: rgba(10, 41, 70, 0.25);

            .title {
                width: 245px;
                height: 38px;
                background: url(./images/daping_04.png) no-repeat;
                background-size: 100% 100%;
            }

            .synthesize {
                margin-top: 20px;
                display: flex;
                justify-content: center;
                align-content: center;

                >img {
                    width: 50px;
                    height: 50px;
                }

                .nmb {
                    margin-left: 22px;
                    color: #8B9096;

                    >span {
                        width: 90px;
                        height: 16px;
                        font-size: 16px;
                        font-weight: 400;
                        color: #00AAFB;
                    }

                    p {
                        font-size: 12px;
                        font-weight: 400;
                        color: #8B9096;
                    }
                }
            }

            .branch {
                list-style: none;
                display: flex;
                flex-wrap: wrap;
                align-content: center;

                li {
                    margin-left: 38px;
                    width: 160px;
                    margin-top: 24px;
                    display: flex;
                    flex-wrap: wrap;
                    align-content: center;

                    >img {
                        width: 52px;
                        height: 52px;
                    }

                    .nmb {
                        padding-top: 5px;
                        margin-left: 11px;
                        color: #8B9096;

                        >span {
                            width: 90px;
                            height: 16px;
                            font-size: 16px;
                            font-weight: 400;
                            color: #00AAFB;
                        }

                        p {
                            font-size: 12px;
                            font-weight: 400;
                            color: #8B9096;

                            i {
                                display: inline-block;
                                width: 6px;
                                height: 10px;
                                background: url(./images/sh.png) no-repeat;
                                background-size: 100% 100%;
                                vertical-align: middle;
                            }
                        }
                    }
                }
            }

        }

        .unitOutput {
            margin-top: 17px;
            width: 436px;
            height: 544px;
            border-top: 2px solid #09375D;
            background: rgba(10, 41, 70, 0.25);

            .title {
                width: 245px;
                height: 38px;
                background: url(./images/daping_12.png) no-repeat;
                background-size: 100% 100%;
            }
        }

    }

    .center {
        display: inline-block;
        width: 977px;
        height: 911px;
        margin: 0 14px;
        overflow: hidden;

        .top {
            display: flex;
            width: 800px;
            height: 60px;
            margin: 0 auto;

            >img {
                width: 60px;
                height: 60px;
            }

            ul {
                list-style: none;
                display: flex;
                margin-left: 38px;

                li {
                    width: 160px;
                    color: #fff;
                    margin-left: 16px;

                    .text {
                        font-size: 16px;
                        margin-top: 3px;
                        color: #D3F0FB;


                        i {
                            display: inline-block;
                            width: 9px;
                            height: 16px;
                            background: url(./images/jiantou.png) no-repeat;
                            background-size: 100% 100%;
                        }
                    }

                    .number {
                        margin-top: 3px;

                        span {
                            font-size: 28px;
                            font-weight: bold;
                            color: #43E7FF;
                        }

                        p {
                            display: inline-block;
                            color: #46EDE8;
                            margin-left: 9px;
                            margin-right: 17px;
                        }
                    }


                }
            }
        }

        #mapDiv {}

        .ranking {
            width: 977px;
            height: 234px;
            display: flex;
            justify-content: space-between;

            .rankingList {
                width: 481px;
                height: 232px;
                background: rgba(10, 41, 70, 0.25);
                border-top: 2px solid #09375D;

                .title {
                    width: 245px;
                    height: 38px;
                    background: url(./images/daping_12.png) no-repeat;
                    background-size: 100% 100%;
                }

                table {
                    margin-top: 20px;
                    padding: 0 17px;
                    color: #fff;


                    th {
                        text-align: left;
                        font-size: 16px;
                        font-weight: bold;
                        color: #71CDF9;
                        line-height: 28px;
                    }

                    :nth-child(3) {
                        text-align: right;
                    }

                    td {
                        text-align: left;
                        font-size: 16px;
                        color: rgba(255, 255, 255, .8);
                        font-family: SourceHanSansCN;
                        font-weight: 400;
                        line-height: 31px;

                        img {
                            vertical-align: middle;
                        }
                    }

                }
            }

            .trade {
                .title {
                    width: 245px;
                    height: 38px;
                    background: url(./images/daping_10.png) no-repeat;
                    background-size: 100% 100%;
                }
            }
        }

    }

    .right {
        display: inline-block;
        overflow: hidden;

        .structure {
            width: 436px;
            height: 350px;
            border-top: 2px solid #09375D;
            background: rgba(10, 41, 70, 0.25);

            .title {
                width: 245px;
                height: 38px;
                background: url(./images/daping_06.png) no-repeat;
                background-size: 100% 100%;
            }
        }

        .industry {
            margin-top: 17px;
            width: 436px;
            height: 544px;
            border-top: 2px solid #09375D;
            background: rgba(10, 41, 70, 0.25);

            .title {
                width: 245px;
                height: 38px;
                background: url(./images/daping_10.png) no-repeat;
                background-size: 100% 100%;
            }
        }


    }

}
</style>
