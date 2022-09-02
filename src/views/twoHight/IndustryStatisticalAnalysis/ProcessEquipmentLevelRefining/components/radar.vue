<template>
  <div class="visibleDiv">
    <div id="radar" :style="{width: '100%', height: '380px'}"></div>
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
      let myChart1 = this.$echarts.init(document.getElementById('radar'));
      // 绘制图表
      myChart1.setOption(
        {
          title: {
            text: '',
            subtext: '',
            top: 10,
            left: 10
          },
          tooltip: {
            trigger: 'item'
          },
          color: ['#A878F9', '#3BF4BC'],
          legend: {
            orient: 'vertical',
            type: 'scroll',
            left: 'right',
            top: 'center',
            right: -10,
            data: ['2021年', '2022年']
          },
          /*  visualMap: {
            top: 'middle',
            right: 10,
            color: ['red', 'yellow'],
            calculable: true
          }, */
          radar: {
            indicator: [
              { text: '汽油', max: 400 },
              { text: '煤油', max: 400 },
              { text: '柴油', max: 400 },
              { text: '石脑油', max: 400 },
              { text: '溶剂油', max: 400 },
              { text: '燃料油', max: 400 },
              { text: '石油', max: 400 },
              { text: '沥青', max: 400 },
              { text: '乙烯', max: 400 },
              { text: 'PX', max: 400 },
              { text: '液化气', max: 400 },
              { text: '其他', max: 400 }
            ]
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
    }
  },
  props: {}
}
</script>
<style lang="scss" scoped>
.visibleDiv {
  width: 100%;
  height: 420px;
}
</style>
