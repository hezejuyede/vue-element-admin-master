<template>
  <div class="management-container">
    <left :leftState="leftState" @showLeft="showRight"></left>
    <div :class="leftState ? 'right-show':'right-hide'">
      <div class="containerTop">
        <div class="managementTitle">
          <div class="managementTitleL">
            <div class="">
              <img src="./img/titleImg.png" alt="">
            </div>
            <div class="">
              综合信息展示
            </div>
          </div>
          <div class="managementTitleR">
            <div class="">2022年-08月</div>
          </div>
        </div>
        <details-div></details-div>
      </div>
      <div class="containerBottom">
        <div class="containerBottomT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                工业设备参数
              </div>
            </div>
            <div class="managementTitleR"></div>
          </div>
          <table-div></table-div>
        </div>
        <div class="containerBottomT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
               产品产量
              </div>
            </div>
            <div class="managementTitleR"></div>
          </div>
          <bar-div></bar-div>
        </div>
        <div class="containerBottomT2">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                工业能效指标
              </div>
            </div>
            <div class="managementTitleR">
              <label style="margin-right: 1px;margin-left: 1px" class="fl">
                <el-input v-model.trim="enterpriseName" style="width: 200px" maxlength="20" placeholder="名称"></el-input>
              </label>
              <label style="margin-right: 1px;margin-left: 1px" class="fl">
                <el-select
                  style="width:150px"
                  v-model="type"
                  clearable
                  filterable
                  allow-create
                  collapse-tags
                  default-first-option
                  placeholder="类型">
                  <el-option
                    v-for="item in typeOptions"
                    :key="item.id"
                    :label="item.name"
                    :value="item.id">
                  </el-option>
                </el-select>
              </label>
              <label style="margin-right: 1px;margin-left: 1px" class="fl">
                <el-date-picker style="width: 240px" v-model="examineTime3" type="daterange"
                                start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
                </el-date-picker>
              </label>
            </div>
          </div>
          <line-div></line-div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import left from './common/left'
import detailsDiv from './components/details'
import tableDiv from './components/table'
import lineDiv from './components/line'
import barDiv from './components/bar'
export default {
  name: 'RegisterDiv',
  data() {
    return {
      leftState: true,
      enterpriseName: '',
      examineTime: [],
      type: '',
      typeOptions: [
        {"name": "封顶", "id": "1"},
        {"name": "捣固", "id": "2"}
      ]
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
  components: { left, detailsDiv, tableDiv, lineDiv, barDiv },

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
.el-badge__content.is-fixed {
  right: 0
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
    height: 170px;
    width: 100%;
    background-color: #ffffff;
  }

  .containerBottom {
    width: 100%;
    height: 730px;

    .containerBottomT {
      width: 49%;
      height: 350px;
      float: left;
      background-color: #ffffff;
      margin-right: 1%;
      margin-top: 15px;
    }
    .containerBottomT2{
      width: 99%;
      height: 350px;
      float: left;
      background-color: #ffffff;
      margin-right: 1%;
      margin-top: 15px;
    }
  }

}

</style>
