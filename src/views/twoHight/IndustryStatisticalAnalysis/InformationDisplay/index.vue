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
              归上工业增加值
            </div>
          </div>
          <div class="managementTitleR"></div>
        </div>
        <list-div></list-div>
      </div>
      <div class="containerBottom">
        <div class="containerBottomL">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                统计对比
              </div>
            </div>
            <div class="managementTitleR"></div>
          </div>
          <descriptions-div></descriptions-div>
        </div>
        <div class="containerBottomR">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                趋势图
              </div>
            </div>
            <div class="managementTitleR">
              <label style="margin-right: 5px;margin-left: 5px" class="fl">
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
              <label style="margin-right: 5px;margin-left: 5px" class="fl">
                <el-date-picker style="width: 240px" v-model="examineTime" type="daterange"
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
</template>

<script>
import left from './common/left'
import listDiv from './components/list'
import descriptionsDiv from './components/descriptions'
import barDiv from './components/bar'
export default {
  name: 'RegisterDiv',
  data() {
    return {
      leftState: true,
      examineTime: [],
      type: '',
      typeOptions: [
        {"name": "增加值总总额", "id": "1"},
        {"name": "劳动者报酬", "id": "2"},
        {"name": "固定资产折旧", "id": "3"},
        {"name": "生产税净值", "id": "4"},
        {"name": "营业余额", "id": "5"}
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
  components: { left, listDiv, descriptionsDiv, barDiv},

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
    height: 430px;
    margin-bottom: 20px;
    background-color: #ffffff;
  }
  .containerBottom {
    height: 450px;
    .containerBottomL {
      width: 49%;
      height: 100%;
      background-color: #ffffff;
      margin-right: 1%;
      float: left;
    }
    .containerBottomR {
      width: 49%;
      height: 100%;
      background-color: #ffffff;
      margin-right: 1%;
      float: left;
    }
  }
}

</style>
