<template>
  <div class="visibleDiv">
    <div class="bottomT">
      <div class="bottomTTop">
        高熔炉
      </div>
      <div class="bottomTBottom">
        <div class="bottomTTemplate" v-for="(item,index) in listData[0]" :key="index">
          <div class="">{{ item.name }}</div>
          <div>{{ item.number }}</div>
        </div>
      </div>
    </div>
    <div class="bottomT" style="background-color: #ECFAFC">
      <div class="bottomTTop">
        高熔炉
      </div>
      <div class="bottomTBottom">
        <div class="bottomTTemplate" v-for="(item,index) in listData[1]" :key="index" style="background-color: #C1EFF6">
          <div class="">{{ item.name }}</div>
          <div>{{ item.number }}</div>
        </div>
      </div>
    </div>
    <div class="bottomT" style="background-color: #EDFCF9">
      <div class="bottomTTop">
        高熔炉
      </div>
      <div class="bottomTBottom">
        <div class="bottomTTemplate" v-for="(item,index) in listData[2]" :key="index" style="background-color: #C5F6EB">
          <div class="">{{ item.name }}</div>
          <div>{{ item.number }}</div>
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
    width: 30%;
    height: 165px;
    margin-top: 10px;
    box-shadow: 2.5px 2.5px 2.5px #E6F3F3;
    margin-left: 2.5%;
    background-color: #EAF1FF;
    .bottomTTop{
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: flex-start;
      padding-left: 4%;
    }
    .bottomTBottom{
      height: 120px;
      .bottomTTemplate{
        float: left;
        height: 50px;
        width: 28%;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        margin-left: 4%;
        margin-top: 8px;
        background-color: #C5D9FF;

        border-radius: 5px;
        div:first-child{
          flex: 1;
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          justify-content: flex-start;
          padding-left: 10px;
          padding-top: 5px;
          font-size: 12px;
        }
        div:last-child{
          flex: 1;
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          justify-content: flex-end;
          padding-right: 10px;
          font-size: 14px;
          font-weight: bold;
          padding-bottom: 5px;
        }
      }
    }
  }
}

</style>
