<template>
  <div class="visibleDiv">
    <div class="bottomT" v-for="(item,index) in listData" :key="index">
      <div class="bottomTTop">
        高熔炉
      </div>
      <div class="bottomTTemplate" v-for="(item,index) in listData[0]">
        <div class="">{{item.name}}</div>
        <div>{{ item.number }}</div>
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
        [{ 'name': '能效指标', 'number': '5' },
          { 'name': '行业指标', 'number': '6' },
          { 'name': '行业标杆值', 'number': '7' },
          { 'name': '行业排名', 'number': '8' },
          { 'name': '地市排名', 'number': '4' },
          { 'name': '全省排名', 'number': '8' }],
        [{ 'name': '能效指标', 'number': '5' },
          { 'name': '行业指标', 'number': '6' },
          { 'name': '行业标杆值', 'number': '7' },
          { 'name': '行业排名', 'number': '8' },
          { 'name': '地市排名', 'number': '4' },
          { 'name': '全省排名', 'number': '8' }],
        [{ 'name': '能效指标', 'number': '5' },
          { 'name': '行业指标', 'number': '6' },
          { 'name': '行业标杆值', 'number': '7' },
          { 'name': '行业排名', 'number': '8' },
          { 'name': '地市排名', 'number': '4' },
          { 'name': '全省排名', 'number': '8' }]
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
    width: 18.5%;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 10px;
    background-color: #ffffff;
    box-shadow: 2.5px 2.5px 2.5px #E6F3F3;
    margin-left: 1%;
    .bottomTL {
      flex: 1;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: flex-start;
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
