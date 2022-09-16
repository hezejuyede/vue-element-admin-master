<template>
  <!-- <v-scale-screen width="1920" height="1080"> -->
  <ScaleBox>
    <div class="content">
      <div class="bg">
        <img src="./image/daping_01.png" alt="" class="title">
        <div style="position:relative; height: 30px">
          <span class="time">{{ date }} {{ week }}</span>
        </div>
        <div class="flex">
          <div style="height: 100%">
            <div class="left-top">
              <div class="border">
                <img src="./image/icon1.png" alt="">
              </div>
              <div id="chartPie" class="pie-wrap" />
            </div>
            <div class="left-bottom">
              <div class="border">
                <img src="./image/icon2.png" alt="">
              </div>
              <div id="chartHistogram" class="histogram-wrap" />
            </div>
          </div>
          <div style="width: 100%; position: relative;">
            <img v-if="city === '山东省'" src="./image/青岛_03.jpg" alt="" style="width: 100%;">
            <img v-if="city === '济南市'" src="./image/济南市_01.jpg" alt="" style="width: 100%;">
            <img v-if="city === '钢城区'" src="./image/钢城区_01.jpg" alt="" style="width: 100%;">
            <img v-if="city === '山东钢铁股份莱芜分公司(含银山型钢)'" src="./image/山钢公司_01.jpg" alt="" style="width: 100%;">
            <img v-if="city === '青岛市'" src="./image/青岛_03.jpg" alt="" style="width: 100%;">
            <img v-if="city === '淄博市'" src="./image/淄博_03.jpg" alt="" style="width: 100%;">
            <img v-if="city === '枣庄市'" src="./image/枣庄_03.jpg" alt="" style="width: 100%;">
            <img v-if="city === '东营市'" src="./image/东营_03.jpg" alt="" style="width: 100%;">
            <img v-if="city === '烟台市'" src="./image/烟台_03.jpg" alt="" style="width: 100%;">
            <img v-if="city === '滨州市'" src="./image/滨州_03.jpg" alt="" style="width: 100%;">
            <div v-show="expandShow" class="button">
              <img src="./image/expand2.png" alt="" @click="expandClick">
            </div>
            <div class="img">
              <img src="./image/xiangm-dt_07.png" alt="">
              <img src="./image/xiangm-dt_10.png" alt="">
              <img src="./image/xiangm-dt_13.png" alt="">
              <img src="./image/xiangm-dt_16.png" alt="">
              <img src="./image/xiangm-dt_22.png" alt="">
              <img src="./image/xiangm-dt_26.png" alt="">
              <img src="./image/xiangm-dt_30.png" alt="">
              <img src="./image/xiangm-dt_33.png" alt="">
            </div>
            <div v-show="centerShow" class="center tree">
              <img src="./image/expand1.png" alt="" @click="centerClick">
              <div style="margin-top: 15px; margin-bottom: 13px;">
                <el-input v-model="input3" placeholder="输入关键字进行过滤" size="medium" class="input-with-select">
                  <el-button slot="append" icon="el-icon-search" />
                </el-input>
              </div>
              <el-tree :data="data" :props="defaultProps" highlight-current node-key="id" :default-expanded-keys="[1,2,9,17,10]" @node-click="handleNodeClick" />
            </div>
            <div class="div">
              <div class="smTitle">
                <img src="./image/xiangm-dt_41.png" alt="">
                <div>
                  <span>2617</span>
                  <p>企业及项目总数</p>
                </div>
              </div>
              <div id="radar" class="radar-wrap" />
            </div>
          </div>
          <div />
        </div>
      </div>
    </div>
  </ScaleBox>
<!-- </v-scale-screen> -->
</template>

<script>
import * as echarts from 'echarts'
require('echarts/theme/macarons')
import Vue from 'vue'
import ScaleBox from './scaleBox/index.vue'
// import VScaleScreen from 'v-scale-screen'
// Vue.use(VScaleScreen)
export default {
  name: 'LargeScreen',
  components: {
    // VScaleScreen,
    ScaleBox
  },
  data() {
    return {
      total: 5308,
      input3: '',
      expandShow: true,
      centerShow: false,
      timer: null,
      date: '',
      week: '',
      city: '济南市',
      // 省市tree结构
      data: [{
        id: 1,
        label: '山东省',
        children: [{
          id: 2,
          label: '济南市',
          children: [{
            id: 10,
            label: '钢城区',
            children: [{
              id: 18,
              label: '山东钢铁股份莱芜分公司(含银山型钢)'
            }]
          }]
        },
        {
          id: 3,
          label: '青岛市',
          children: [{
            id: 12,
            label: '黄岛区'
          }]
        },
        {
          id: 4,
          label: '淄博市',
          children: [{
            id: 12,
            label: '长店区'
          }]
        },
        {
          id: 5,
          label: '枣庄市',
          children: [{
            id: 13,
            label: '台儿庄区'
          }]
        },
        {
          id: 6,
          label: '东营市',
          children: [{
            id: 14,
            label: '河口区'
          }]
        },
        {
          id: 7,
          label: '烟台市',
          children: [{
            id: 15,
            label: '蓬莱区'
          }]
        },
        {
          id: 8,
          label: '滨州市',
          children: [{
            id: 16,
            label: '邹平县'
          }]
        }]
      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  mounted() {
    this.drawPieChart()
    this.drawHistogramChart()
    this.radar()
    this.dateFormat()
    this.timer = setInterval(() => {
      this.dateFormat()
    }, 1000)
  },
  methods: {
    handleNodeClick(data) {
      console.log('!!--->', data)
      this.city = data.label
    },
    // 获取当前时间和星期
    dateFormat() {
      const date = new Date()
      const year = date.getFullYear()
      const month =
        date.getMonth() + 1 < 10
          ? '0' + (date.getMonth() + 1)
          : date.getMonth() + 1
      const day = date.getDate() < 10 ? '0' + date.getDate() : date.getDate()
      this.date = year + '-' + month + '-' + day + ' '
      this.week = '星期' + '日一二三四五六'.charAt(date.getDay())
    },
    // 饼状图
    drawPieChart() {
      var total = this.total
      this.chartPie = echarts.init(
        document.getElementById('chartPie'),
        'macarons'
      )
      this.chartPie.setOption({
        title: {
          zlevel: 0,
          text: [
            '{value|' + total + '}'
          ].join('\n'),
          rich: {
            value: {
              color: '#ffffff',
              fontSize: 16,
              fontWeight: 'bold',
              lineHeight: 40
            },
            name: {
              color: '#909399',
              lineHeight: 20
            }
          },
          left: '25%',
          top: '38%',
          textStyle: {
            rich: {
              value: {
                color: '#909399',
                fontSize: 16,
                fontWeight: 'bold',
                lineHeight: 40
              },
              name: {
                color: '#909399',
                lineHeight: 20
              }
            }
          }
        },
        color: [
          '#33CCCC',
          '#30AEDA',
          '#0669B6',
          '#34329C',
          '#211B63',
          '#6B2D90',
          '#932F8E',
          '#9B035F',
          '#C62C33',
          '#E1262C',
          '#E95A2E',
          '#F69C2A',
          '#EFE122',
          '#89C238',
          '#37B244',
          '#339966'
        ],
        tooltip: {
          trigger: 'item'
        },
        legend: {
          orient: 'vertical',
          right: '10%',
          top: '20%',
          itemWidth: 8,
          itemHeight: 8,
          textStyle: {
            color: '#999',
            fontSize: 16
          }
        },
        series: [
          {
            name: '区域数量',
            type: 'pie',
            radius: ['30%', '60%'],
            center: ['30%', '45%'],
            avoidLabelOverlap: false,
            label: {
              // 不显示标签文字
              show: false,
              position: 'center'
              // normal: {
              //   position: 'inner',
              //   formatter: '{c}'
              // }
            },
            labelLine: {
              show: false
            },
            data: [
              { value: 402, name: '济南' },
              { value: 428, name: '青岛' },
              { value: 321, name: '淄博' },
              { value: 135, name: '东营' },
              { value: 168, name: '枣庄' },
              { value: 356, name: '烟台' },
              { value: 356, name: '潍坊' },
              { value: 215, name: '济宁' },
              '\n',
              { value: 401, name: '泰安' },
              { value: 323, name: '威海' },
              { value: 321, name: '日照' },
              { value: 335, name: '滨州' },
              { value: 268, name: '德州' },
              { value: 356, name: '聊城' },
              { value: 556, name: '临沂' },
              { value: 367, name: '菏泽' }
            ]
          }
        ]
      })
    },
    // 柱状图
    drawHistogramChart() {
      const data = [220, 182, 191, 234, 290, 330, 310, 123, 442, 321, 90, 149, 210, 122, 133, 334, 198, 123, 125, 220]
      const yMax = 500
      const dataShadow = []
      for (let i = 0; i < data.length; i++) {
        dataShadow.push(yMax)
      }
      this.chartHistogram = echarts.init(
        document.getElementById('chartHistogram'),
        'macarons'
      )
      this.chartHistogram.setOption({
        xAxis: {
          data: ['铸造', '轮胎', '煤加工', '煤电', '钢铁', '炼化', '焦化', '石灰', '水泥', '化学原料', '陶瓷', '玻璃', '铁合金', '有色', '防水建材', '肥料'],
          axisLabel: {
            interval: 0, // 横轴信息全部显示
            rotate: -100, // 100度角倾斜显示
            textStyle: {
              color: ' #FFFFFF',
              fontSize: 14
            }
          },
          axisLine: {
            lineStyle: {
              color: ' #FFFFFF',
              line: 1
            }
          }
        },
        grid: {
          x: 40,
          y: 50,
          x2: 5,
          y2: 65,
          borderWidth: 1
        },
        yAxis: {
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            color: '#FFFFFF',
            textStyle: {
              fontSize: 14
            }
          }
        },
        dataZoom: [
          {
            type: 'inside'
          }
        ],
        series: [
          {
            type: 'bar',
            showBackground: true,
            barWidth: 10, // 柱子宽度
            itemStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: '#04CECB' },
                { offset: 1, color: '#131D21' }
              ])
            },
            data: data
          }
        ]
      })
    },
    // 雷达图
    radar() {
      this.myChart1 = echarts.init(document.getElementById('radar'))
      // 绘制图表
      this.myChart1.setOption(
        {
          title: {
            text: '',
            subtext: '',
            top: 0,
            left: 0
          },
          color: ['#A878F9', '#3BF4BC'],
          legend: {
            y: 'bottom',
            x: 'center',
            bottom: 0,
            icon: 'circle',
            itemHeight: 14,
            itemWidth: 14,
            padding: [10, 0, 0, 0],
            data: ['2021年', '2022年'],
            textStyle: {
              color: 'rgb(255,255,255,0.9)',
              fontSize: 16
            }
          },
          tooltip: {
            trigger: 'item',
            textStyle: {
              fontSize: 16, // 字体大小
              color: '#ffffff'
            }
          },
          radar: {
            indicator: [
              { text: '济南', max: 400 },
              { text: '青岛', max: 400 },
              { text: '淄博', max: 400 },
              { text: '东营', max: 400 },
              { text: '枣庄', max: 400 },
              { text: '烟台', max: 400 },
              { text: '潍坊', max: 400 },
              { text: '沥青', max: 400 },
              { text: '济宁', max: 450 },
              { text: '泰安', max: 400 },
              { text: '威海', max: 400 },
              { text: '日照', max: 400 },
              { text: '滨州', max: 400 },
              { text: '德州', max: 400 },
              { text: '聊城', max: 400 },
              { text: '临沂', max: 400 },
              { text: '菏泽', max: 400 }
            ],
            name: {
              textStyle: {
                padding: [-8, -14], // 控制文字padding
                fontSize: 16 // 控制文本的大小
              }
            }
          },
          series: [
            {
              name: 'Budget vs spending',
              type: 'radar',
              data: [
                {
                  value: [390, 140, 280, 260, 220, 210, 220, 300, 200, 350, 232, 180],
                  name: '2022年',
                  label: {
                    show: true
                  },
                  symbol: 'none',
                  smooth: true,
                  areaStyle: {
                    color: '#3BF4BC'
                  }
                },
                {
                  value: [320, 300, 200, 350, 232, 180, 280, 380, 380, 190, 270, 350],
                  name: '2021年',
                  label: {
                    show: true
                  },
                  symbol: 'none',
                  smooth: true,
                  areaStyle: {
                    color: '#A878F9'
                  }
                }
              ]
            }
          ]
        }, true)
    },
    expandClick() {
      this.centerShow = true
      this.expandShow = false
    },
    centerClick() {
      this.centerShow = false
      this.expandShow = true
    }
  }
}
</script>
<style lang="scss" scoped>
.content{
  width: 100%;
  height: 100%;
  .bg{
    width: 100%;
    height: 100%;
    position: relative;
    background: url("~./image/bg.png") no-repeat;
    overflow: hidden;
    background-size: cover;
    .time{
      color: #fff;
      font-style: 16px;
      position: absolute;
      right: 10px;
    }
    .flex{
      display: flex;
      height: 100%;
    }
    .button{
      padding: 10px;
      background-color: rgba(0,0,0,0.2);
      position: absolute;
      top: 0;
      img{
        width: 30px;
        height: 23px;
      }
    }
    .img :nth-child(1)	{
      position: absolute;
      top: 300px;
      left: 600px;
    }
    .img :nth-child(2)	{
      position: absolute;
      top: 430px;
      left: 460px;
    }
    .img :nth-child(3)	{
      position: absolute;
      top: 200px;
      left: 600px;
    }
    .img :nth-child(4)	{
      position: absolute;
      top: 260px;
      left: 800px;
    }
    .img :nth-child(5)	{
      position: absolute;
      top: 350px;
      left: 400px;
    }
    .img :nth-child(6)	{
      position: absolute;
      top: 600px;
      left: 500px;
    }
    .img :nth-child(7)	{
      position: absolute;
      top: 100px;
      left: 500px;
    }
    .img :nth-child(8)	{
      position: absolute;
      top: 430px;
      left: 600px;
    }
    .center{
      width: 283px;
      height: 911px;
      background: #0A213D;
      box-shadow: 8px 0px 19px 2px rgba(0,0,0,0.13);
      margin: 1px 0px 0px 1px;
      padding: 10px 10px 0px 10px;
      position: absolute;
      top: 0;
      img{
        width: 30px;
        height: 23px;
      }
      ::v-deep.el-input__inner{
        background-color: transparent;
        color: #999;
      }
      ::v-deep.el-input-group__append, .el-input-group__prepend {
        background-color: transparent;
      }
      ::v-deep .el-tree--highlight-current .el-tree-node.is-current > .el-tree-node__content {
        // 设置颜色
        background-color:  rgba(0,0,0,0.2)!important;
      }
      ::v-deep .el-tree{
        background-color: transparent;
        color: #999;
      }
      ::v-deep .el-tree-node__label {
        font-family: Microsoft YaHei;
        font-weight: 400;
        font-size: 16px;
        color: #fff
      }
      ::v-deep.el-tree-node {
        white-space: normal;

        .el-tree-node__content {
          height: 100%;
          padding-top: 5px;
          padding-bottom: 5px;
        }
      }
      ::v-deep.el-tree-node__content{
          &:hover{
          background-color: rgba(0,0,0,0.2);
        }
      }
    }
  .left-top{
    padding: 0px 10px 0px 10px;
    width: 536px;
    height: 410px;
  .border{
    border-top: 1px solid #09375D ;
  }
  }
  .left-bottom{
    padding: 0px 10px 0px 10px;
    width: 536px;
    .border{
      border-top: 1px solid #09375D ;
    }
  }
  .title{
    width: 100%;
  }
  .pie-wrap {
    width: 100%;
    height: 410px;
  }
  .histogram-wrap {
    width: 100%;
    height: 484px;
  }
  .div{
    position: absolute;
    right: 30px;
    bottom: 150px;
    background: url("~./image/fceng.png") no-repeat;
    background-size: 100% 100%;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 10px;
    .smTitle{
      display: flex;
      align-items: center;
      justify-content: center;
      padding-top: 10px;
    }
    span{
      font-size: 19px;
      font-family: PangMenZhengDao;
      font-weight: 400;
      color: #FFFFFF;
    }
    p{
      margin: 0;
      font-size: 19px;
      font-family: Microsoft YaHei;
      color: #FFFFFF;
    }
    .radar-wrap{
      width: 351px;
      height: 409px;
      padding: 10px;
    }
    img{
      width: 45px;
      height: 44px;
      margin-right: 6px;
    }
  }
  .text {
    font-size: 14px;
  }
  .item {
    margin-bottom: 18px;
  }
  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both
  }
  .box-card {
    width: 380px;
  }
  }
}
</style>
