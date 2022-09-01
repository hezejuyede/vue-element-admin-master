<template>
  <div class="visibleDiv">
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
</template>

<script type="text/ecmascript-6">
export default {
  name: 'Modal1',
  data() {
    return {
      listData: [
        { 'img': require('../images/icon1.png'), 'name': ' 企业名称', 'number': '7' },
        { 'img': require('../images/icon2.png'), 'name': '统一社会信用代码', 'number': '7' },
        { 'img': require('../images/icon3.png'), 'name': '所属城市', 'number': '7' },
        { 'img': require('../images/icon4.png'), 'name': '所属县区', 'number': '7' },
        { 'img': require('../images/icon5.png'), 'name': '企业详细地址', 'number': '济南市历下区龙鼎大道1号龙奥大厦5层济南市历下区龙鼎大道1号龙奥大厦5层' },
        { 'img': require('../images/icon6.png'), 'name': '地理位置', 'number': '7' },
        { 'img': require('../images/icon7.png'), 'name': '企业性质', 'number': '7' },
        { 'img': require('../images/icon8.png'), 'name': '行业归属', 'number': '7' },
        { 'img': require('../images/icon9.png'), 'name': '法定代表人', 'number': '7' },
        { 'img': require('../images/icon10.png'), 'name': '联系电话', 'number': '7' },
        { 'img': require('../images/icon11.png'), 'name': '邮箱', 'number': '7' },
        { 'img': require('../images/icon12.png'), 'name': '用户名', 'number': '7' },
        { 'img': require('../images/icon13.png'), 'name': '实际控制人', 'number': '7' },
        { 'img': require('../images/icon14.png'), 'name': '企业联系人', 'number': '7' },
        { 'img': require('../images/icon15.png'), 'name': '联系电话', 'number': '7' },
        { 'img': require('../images/icon16.png'), 'name': '企业状态', 'number': '7' },
        { 'img': require('../images/icon17.png'), 'name': '是否燃煤', 'number': '7' },
        { 'img': require('../images/icon18.png'), 'name': '是否纳税企业', 'number': '7' },
        { 'img': require('../images/icon19.png'), 'name': '是否上市企业', 'number': '7' },
        { 'img': require('../images/icon20.png'), 'name': '是否已实名认证', 'number': '7' }
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
  .bottomT{
    float: left;
    width: 25%;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 10px;
    .bottomTL{
      flex:1;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: flex-start;
      padding-left: 20px;
    }
    .bottomTR{
      flex: 3;
      height: 100%;
      display: flex;
      align-items: flex-start;
      justify-content: center;
      flex-direction: column;
      div:first-child{
        flex: 1.1;
        width: 100%;
        height: 100%;
        color: #A6AAB0;
        font-size: 14px;
        display: flex;
        align-items: flex-end;
        justify-content: flex-start;
        padding-bottom: 2px;
      }
      div:last-child{
        flex: 1.4;
        width: 100%;
        height: 100%;
        color: #283650;
        font-size: 14px;
        font-weight: bold;
        overflow: hidden;
        text-overflow: ellipsis;
        display:-webkit-box;
        -webkit-box-orient:vertical;
        -webkit-line-clamp:2;
      }
    }
  }
}

</style>
