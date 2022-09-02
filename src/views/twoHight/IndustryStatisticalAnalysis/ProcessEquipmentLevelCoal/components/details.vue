<template>
  <div class="visibleDiv">
    <div class="bottomT" v-for="(item,index) in listData" :key="index">
      <div :style="{'color': item.color}">{{ item.number }}</div>
      <div class="">{{ item.name }}</div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  name: 'Modal1',
  data() {
    return {
      listData: [
        { 'name': '能效指标', 'number': '1', 'color': '#FFA00B' },
        { 'name': '行业指标', 'number': '2', 'color': '#2960FF' },
        { 'name': '行业标杆值', 'number': '3', 'color': '#40CDAE' },
        { 'name': '地市同行业排名', 'number': '4', 'color': '#6D74FF' },
        { 'name': '省内同行业排名', 'number': '5', 'color': '#0BB1FE' },
        { 'name': '地市排名', 'number': '6', 'color': '#FFA00B' },
        { 'name': '全省排名', 'number': '7', 'color': '#CC76FE' }
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
    width: 12%;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    margin-top: 10px;
    background-color: #F3FCFD;
    margin-left: 2%;
    border-bottom:3px solid #409EFF;

    div:first-child {
      font-size: 26px;
      font-weight: bold;
    }

    div:last-child {
      font-size: 14px;
      font-weight: bold;
      color: #585A5A;
    }

  }
}

</style>
