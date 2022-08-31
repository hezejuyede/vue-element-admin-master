<template>
  <div class="visibleDiv">
    <div class="visibleDivTop">
      <div class="topDiv">
        <div class="topDivL">
          <img src="../images/tu-b_01.png" alt="">
        </div>
        <div class="topDivR">
          <div class="">2617</div>
          <div class="">企业及项目总数</div>
        </div>
      </div>
    </div>
    <div class="visibleDivBottom">
      <div class="bottomT" v-for="(item,index) in listData" :key="index" >
        <div class="bottomTL">
          <img :src="item.img" alt="">
        </div>
        <div class="bottomTR">
          <div class="">{{item.name}}</div>
          <div class="">{{item.number}}</div>
        </div>
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
        { 'img': require('../images/tu-b_02.png'), 'name': '钢铁', 'number': '7' },
        { 'img': require('../images/tu-b_03.png'), 'name': '炼化', 'number': '37' },
        { 'img': require('../images/tu-b_04.png'), 'name': '焦化', 'number': '947' },
        { 'img': require('../images/tu-b_05.png'), 'name': '煤电', 'number': '37' },
        { 'img': require('../images/tu-b_06.png'), 'name': '肥料', 'number': '157' },
        { 'img': require('../images/tu-b_07.png'), 'name': '有色', 'number': '363' },
        { 'img': require('../images/tu-b_08.png'), 'name': '水泥', 'number': '363' },
        { 'img': require('../images/tu-b_09.png'), 'name': '石灰', 'number': '128' },
        { 'img': require('../images/tu-b_10.png'), 'name': '玻璃', 'number': '947' },
        { 'img': require('../images/tu-b_11.png'), 'name': '铸造', 'number': '471' },
        { 'img': require('../images/tu-b_12.png'), 'name': '轮胎', 'number': '507' },
        { 'img': require('../images/tu-b_13.png'), 'name': '陶瓷', 'number': '7' },
        { 'img': require('../images/tu-b_14.png'), 'name': '煤加工', 'number': '471' },
        { 'img': require('../images/tu-b_15.png'), 'name': '铁合金', 'number': '507' },
        { 'img': require('../images/tu-b_16.png'), 'name': '化学原料', 'number': '128' },
        { 'img': require('../images/tu-b_17.png'), 'name': '防水建材', 'number': '157' }
      ]
    }
  },
  mounted() {
    this.getList()
  },
  created() {},
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
  .visibleDivTop{
    width: 95%;
    margin: 0 auto;
    height: 70px;
    border-bottom: 2px solid #D3D3D3;
    display: flex;
    align-items: center;
    justify-content: center;
    .topDiv{
      width: 300px;
      height: 50px;
      display: flex;
      align-items: center;
      justify-content: center;
      .topDivR{
        padding-left: 20px;
        div:first-child{
          font-size: 24px;
          font-weight: bold;
        }
        div:last-child{
          font-size: 12px;
          color: #969BA2;
        }
      }
    }
  }
  .visibleDivBottom{
    .bottomT{
      float: left;
      width: 25%;
      height: 60px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-top: 15px;
      .bottomTL{
        flex:1;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-end;
      }
      .bottomTR{
        flex: 1;
        height: 100%;
        display: flex;
        align-items: flex-start;
        justify-content: center;
        flex-direction: column;
        padding-left: 10px;
        div:first-child{
          color: #A6AAB0;
          font-size: 14px;
        }
        div:last-child{
          color: #283650;
          font-size: 24px;
          font-weight: bold;
        }
      }
    }

  }
}

</style>
