<template>
  <div class="visibleDiv">
    <div class="bottomT" v-for="(item,index) in listData" :key="index">
      <div class="bottomTL">
        <img :src="item.img" alt="">
      </div>
      <div class="bottomTR">
        <div class="">
          <div>{{ item.number }}</div>
          <div style="color: #00B000">+{{ item.compare }}</div>
        </div>
        <div class="">{{ item.name }}</div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  name: 'Modal1',
  data() {
    return {
      listData: [
        {'img': require('../images/icon1.png'), 'name': '能源消费总量(吨标准煤)', 'number': '5812.00', 'compare': '0.31%'},
        {'img': require('../images/icon2.png'), 'name': '煤品(万吨)', 'number': '5812.00', 'compare': '0.31%'},
        {'img': require('../images/icon3.png'), 'name': '电力(万千瓦时)', 'number': '5812.00', 'compare': '0.31%'},
        {'img': require('../images/icon4.png'), 'name': '油品(万吨)', 'number': '5812.00', 'compare': '0.31%'},
        {'img': require('../images/icon5.png'), 'name': '天然气(万立方米)', 'number': '5812.00', 'compare': '0.31%'},
        {'img': require('../images/icon6.png'), 'name': '热量(百万千焦)', 'number': '5812.00', 'compare': '0.31%'},
        {'img': require('../images/icon7.png'), 'name': '其他', 'number': '5812.00', 'compare': '0.31%'},
        {'img': require('../images/icon8.png'), 'name': '用水量(吨)', 'number': '5812.00', 'compare': '0.31%'}
      ]
    }
  },
  mounted() {
    this.getList()
  },
  created() {
  },
  methods: {
    getList() {
    }
  },
  props: {}
}
</script>
<style lang="scss" scoped>

.visibleDiv {
  width: 100%;
  height: 100%;

  .bottomT {
    float: left;
    width: 23.5%;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 10px;
    background-color: #ffffff;
    box-shadow: 2.5px 2.5px 2.5px 2.5px #E6F3F3;
    margin-left: 1%;

    .bottomTL {
      flex: 1;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .bottomTR {
      flex: 3;
      height: 100%;
      display: flex;
      align-items: flex-start;
      justify-content: center;
      flex-direction: column;

      div:first-child {
        flex: 1.4;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;

        div:first-child {
          flex: 1;
          color: #192845;
          display: flex;
          font-size: 20px;
          font-weight: bold;
          align-items: flex-end;
          justify-content: flex-start;
          padding-bottom: 5px;

        }

        div:last-child {
          flex: 1;
          color: #192845;
          display: flex;
          align-items: flex-end;
          justify-content: flex-start;
          padding-bottom: 10px;
        }
      }

      div:last-child {
        flex: 1.1;
        width: 100%;
        height: 100%;
        color: #283650;
        font-size: 14px;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2;
      }
    }
  }
}

</style>
