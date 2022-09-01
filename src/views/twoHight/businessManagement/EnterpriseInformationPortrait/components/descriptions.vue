<template>
  <div class="visibleDiv">
    <div class="descriptionsL">
      <div class="descriptionsT">
        <div class="descriptionsT1">
          月上报
        </div>
        <div class="descriptionsT2">
          <div class="descriptionsT2L">
            <div class="">应报项</div>
            <div class="">{{yybx}}</div>
          </div>
          <div class="descriptionsT2R">
            <div class="">时报率</div>
            <div class="">{{ysbl}}</div>
          </div>
        </div>
        <div class="descriptionsT2 colorDiv">
          <div class="descriptionsT2L">
            <div class="">实报项</div>
            <div class="">{{ysbx}}</div>
          </div>
          <div class="descriptionsT2R">
            <div class="">超时率</div>
            <div class="">{{ycsl}}</div>
          </div>
        </div>
      </div>
    </div>
    <div class="descriptionsR">
      <div class="descriptionsT">
        <div class="descriptionsT1">
          季上报
        </div>
        <div class="descriptionsT2">
          <div class="descriptionsT2L">
            <div class="">应报项</div>
            <div class="">{{jybx}}</div>
          </div>
          <div class="descriptionsT2R">
            <div class="">时报率</div>
            <div class="">{{jsbl}}</div>
          </div>
        </div>
        <div class="descriptionsT2 colorDiv">
          <div class="descriptionsT2L">
            <div class="">实报项</div>
            <div class="">{{jsbx}}</div>
          </div>
          <div class="descriptionsT2R">
            <div class="">超时率</div>
            <div class="">{{jcsl}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">

export default {
  name: 'List',
  data() {
    return {
      yybx: '11',
      ysbl: '11',
      ysbx: '11',
      ycsl: '11',

      jybx: '22',
      jsbl: '22',
      jsbx: '22',
      jcsl: '22',
    }
  },
  mounted() {
    this.getList()
  },
  created() {
  },
  methods: {
    getList() {
    },
  },
  props: {}
}
</script>
<style lang="scss" scoped>

.visibleDiv {
  width: 100%;
  height: 110px;
  .descriptionsL {
    float: left;
    width: 50%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .descriptionsR{
    float: left;
    width: 50%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .descriptionsT{
    width: 80%;
    height: 90px;
    border: 1px solid #D9E3EA;
    border-bottom: none;
    .descriptionsT1{
      height: 30px;
      border-bottom:1px solid #D9E3EA;
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: #F4F5F9;
      font-weight: bold;
      font-size: 12px;
      font-weight: bold;
    }
    .descriptionsT2{
      height: 30px;
      border-bottom:1px solid #D9E3EA;
      font-size: 12px;
      font-weight: bold;
      .descriptionsT2L{
        width: 50%;
        height: 30px;
        float: left;
        border-right:1px solid #D9E3EA;
        display: flex;
        align-items: center;
        justify-content: center;
        div:first-child{
          flex: 2;
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          justify-content: center;
        }
        div:last-child{
          flex: 1;
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          justify-content: center;
        }
      }
      .descriptionsT2R{
        width: 50%;
        height: 30px;
        float: left;
        border-right:1px solid #D9E3EA;
        display: flex;
        align-items: center;
        justify-content: center;
        div:first-child{
          flex: 2;
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          justify-content: center;
        }
        div:last-child{
          flex: 1;
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          justify-content: center;
        }
      }
    }
    .colorDiv{
      background-color: #F4F5F9;
    }
  }
}

</style>

