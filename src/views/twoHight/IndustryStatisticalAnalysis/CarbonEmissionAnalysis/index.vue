<template>
  <div class="management-container">
    <left :leftState="leftState" @showLeft="showRight"></left>
    <div :class="leftState ? 'right-show':'right-hide'">
      <div class="containerTop">
        <div class="containerTopT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
              </div>
              <div class="">
                区域碳排放强度
              </div>
            </div>
            <div class="managementTitleR" id="managementTitleR1">
              <label class="fl">
                <el-date-picker style="width: 240px" v-model="examineTime1" type="daterange"
                                start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
                </el-date-picker>
              </label>
            </div>
          </div>
        </div>
        <div class="containerTopT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
              </div>
              <div class="">
                济南市市碳排放地图
              </div>
            </div>
            <div class="managementTitleR">
            </div>
          </div>
        </div>
        <div class="containerTopT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
              </div>
              <div class="">
                行业碳排放强度
              </div>
            </div>
            <div class="managementTitleR">
              <label class="fl" id="managementTitleR2">
                <el-date-picker style="width: 240px" v-model="examineTime2" type="daterange"
                                start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
                </el-date-picker>
              </label>
            </div>
          </div>
        </div>
      </div>
      <div class="containerBottom">
        <div class="containerTopL">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
              </div>
              <div class="">
                区域碳排放占比
              </div>
            </div>
            <div class="managementTitleR">
              <label class="fl" id="managementTitleR2">
                <el-date-picker style="width: 240px" v-model="examineTime2" type="daterange"
                                start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
                </el-date-picker>
              </label>
            </div>
          </div>
          <pei-div></pei-div>
        </div>
        <div class="containerTopR">
          <div class="containerTopRT">
            <div class="managementTitle">
              <div class="managementTitleL">
                <div class="">
                  <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
                </div>
                <div class="">
                  实时碳排放强度
                </div>
              </div>
              <div class="managementTitleR">
              </div>
            </div>
            <line-div></line-div>
          </div>
          <div class="containerTopRB">
            <div class="managementTitle">
              <div class="managementTitleL" style="width: 30%">
                <div class="">
                  <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
                </div>
                <div class="">
                  碳排放统计
                </div>
              </div>
              <div class="managementTitleR" style="width: 70%">
                <div class="" style="width: 400px;height: 100%;display: flex;align-items: center;justify-content: center">
                  <label class="fl">
                    <el-radio-group v-model="emissions">
                      <el-radio label="1">日排放量</el-radio>
                      <el-radio label="2">月排放量</el-radio>
                    </el-radio-group>
                  </label>
                </div>

                <label class="fl">
                  <el-date-picker style="width: 240px" v-model="examineTime2" type="daterange"
                                  start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
                  </el-date-picker>
                </label>
              </div>
            </div>
            <bar-div></bar-div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import left from './common/left'
import barDiv from './components/bar'
import lineDiv from './components/line'
import peiDiv from './components/pie'
export default {
  name: 'RegisterDiv',
  data() {
    return {
      leftState: true,
      examineTime1: [],
      examineTime2: [],
      emissions: '1'
    }
  },
  watch: {
    $route: {
      handler: function(route) {
      },
      immediate: true
    }
  },
  // eslint-disable-next-line vue/no-unused-components
  components: { left, barDiv, lineDiv, peiDiv },

  created() {
  },
  mounted() {
  },
  destroyed() {
  },
  methods: {
    showRight(leftState) {
      this.leftState = leftState
    }
  }
}
</script>
<style lang="scss">
.el-table {
  th {
    padding: 0;
  }

  td {
    padding: 5px;
  }

  ::v-deep .el-range-editor--medium .el-range-input {
    font-size: 12px;
  }
}

</style>
<style lang="scss" scoped>

.management-container {
  width: 100%;
  height: 950px;
  background-color: #F8F8F8;
  padding-top: 20px;

  .managementTitle {
    height: 60px;

    .managementTitleL {
      float: left;
      width: 50%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: flex-start;
      padding-left: 5px;
      font-size: 12px;

      img {
        margin-right: 10px;
      }

      div:last-child {
        font-weight: bold;
      }
    }

    .managementTitleR {
      float: left;
      width: 50%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: flex-end;

      div {
        margin-right: 5px;
        font-weight: bold;
        font-size: 12px;
      }
    }
  }

  .right-show {
    position: absolute;
    width: 80%;
    left: 20%;
    top: 20px;
    height: 800px;
    transition: all 0.5s;
  }

  .right-hide {
    position: absolute;
    width: 98%;
    left: 2%;
    top: 20px;
    height: 800px;
    transition: all 0.5s;
  }

  .containerTop {
    width: 100%;
    height: 350px;
    background-color: #F8F8F8;

    .containerTopT {
      width: 32%;
      height: 350px;
      background-color: #ffffff;
      float: left;
      margin-right: 1%;
    }
  }
  .containerBottom{
    margin-top: 20px;
    height: 530px;
    .containerTopL{
      float: left;
      width: 32%;
      height: 100%;
      background-color: #ffffff;
      margin-right: 1%;
    }
    .containerTopR{
      float: left;
      width: 65%;
      height: 100%;
      .containerTopRT{
        height: 49%;
        margin-bottom: 1.5%;
        background-color: #ffffff;
      }
      .containerTopRB{
        height: 49%;
        background-color: #ffffff;
      }
    }
  }

}

</style>
