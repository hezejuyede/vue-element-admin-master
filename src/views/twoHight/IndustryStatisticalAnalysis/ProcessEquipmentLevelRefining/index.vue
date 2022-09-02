<template>
  <div class="management-container">
    <left :leftState="leftState" @showLeft="showRight"></left>
    <div :class="leftState ? 'right-show':'right-hide'">
      <div class="containerBottom">
        <div class="containerBottomT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                工艺设备参数
              </div>
            </div>
            <div class="managementTitleR"></div>
          </div>
          <iron-table></iron-table>
        </div>
        <div class="containerBottomT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                产量同比
              </div>
            </div>
            <div class="managementTitleR">
              <label style="margin-right: 1px;margin-left: 1px" class="fl">
                <el-date-picker style="width: 240px" v-model="examineTime3" type="daterange"
                                start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
                </el-date-picker>
              </label>
            </div>
          </div>
          <steel-table></steel-table>
        </div>
        <div class="containerBottomT" style="margin-top: 20px">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                工艺能效指标
              </div>
            </div>
            <div class="managementTitleR">
              <label style="margin-right: 1px;margin-left: 1px" class="fl">
                <el-select
                  style="width:120px"
                  v-model="tyepe1"
                  clearable
                  filterable
                  allow-create
                  collapse-tags
                  default-first-option
                  placeholder="类型">
                  <el-option
                    v-for="item in tyepeOptions"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
                  </el-option>
                </el-select>
              </label>
              <label style="margin-right: 1px;margin-left: 1px" class="fl">
                <el-date-picker style="width: 240px" v-model="examineTime1" type="daterange"
                                start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
                </el-date-picker>
              </label>
            </div>
          </div>
          <product-line></product-line>
        </div>
        <div class="containerBottomT" style="margin-top: 20px">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                产品产量
              </div>
            </div>
            <div class="managementTitleR">
              <label style="margin-right: 1px;margin-left: 1px" class="fl">
                <el-date-picker style="width: 240px" v-model="examineTime2" type="daterange"
                                start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
                </el-date-picker>
              </label>
            </div>
          </div>
          <industry-bar></industry-bar>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import left from './common/left'
import industryBar from './components/bar'
import productLine from './components/line'
import ironTable from './components/ironTable'
import steelTable from './components/steelTable'

export default {
  name: 'RegisterDiv',
  data() {
    return {
      leftState: true,
      examineTime1: [],
      examineTime2: [],
      examineTime3: [],
      tyepe1: '',
      tyepe2: '',
      tyepeOptions: [
        {"name": "产值", "id": "1"},
        {"name": "主业营收", "id": "2"},
        {"name": "利润", "id": "3"},
        {"name": "入库税", "id": "4"}
      ]
    }
  },
  watch: {
    $route: {
      handler: function (route) {
      },
      immediate: true
    }
  },
  // eslint-disable-next-line vue/no-unused-components
  components: {left,industryBar, productLine, steelTable, ironTable},

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
      padding-left: 10px;

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
        margin-right: 20px;
        font-weight: bold;
        font-size: 14px;
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
    height: 250px;
    width: 100%;
    background-color: #ffffff;
  }

  .containerBottom {
    width: 100%;
    height: 730px;

    .containerBottomT {
      width: 49%;
      height: 440px;
      float: left;
      background-color: #ffffff;
      margin-right: 1%;
    }
  }
}

</style>
