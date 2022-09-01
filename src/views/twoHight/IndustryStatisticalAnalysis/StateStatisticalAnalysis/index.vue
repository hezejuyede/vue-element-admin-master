<template>
  <div class="management-container">
    <left :leftState="leftState" @showLeft="showRight"></left>
    <div :class="leftState ? 'right-show':'right-hide'">
      <div class="containerTop">
        <div class="managementTitle">
          <div class="managementTitleL">
            <div class="">
              <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
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
                <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
              </div>
              <div class="">
                趋势图
              </div>
            </div>
            <div class="managementTitleR"></div>
          </div>
        </div>
        <div class="containerBottomT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
              </div>
              <div class="">
                能耗强度趋势
              </div>
            </div>
            <div class="managementTitleR"></div>
          </div>
        </div>
        <div class="containerBottomT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
              </div>
              <div class="">
                地域统计分析
              </div>
            </div>
            <div class="managementTitleR"></div>
          </div>
        </div>
        <div class="containerBottomT">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="../StateStatisticalAnalysis/img/titleImg.png" alt="">
              </div>
              <div class="">
                行业统计分析
              </div>
            </div>
            <div class="managementTitleR"></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import left from '../StateStatisticalAnalysis/common/left'
import detailsDiv from '../StateStatisticalAnalysis/components/details'

export default {
  name: 'RegisterDiv',
  data() {
    return {
      leftState: true,
      examineTime1: [],
      examineTime2: [],
      examineTime3: [],
      examineTime4: [],
      industry: '',
      industryOptions: [
        {"name": "增加值总总额", "id": "1"},
        {"name": "劳动者报酬", "id": "2"},
        {"name": "固定资产折旧", "id": "3"},
        {"name": "生产税净值", "id": "4"},
        {"name": "营业余额", "id": "5"}
      ],
      region: '',
      regionOptions: [
        {"name": "增加值总总额", "id": "1"},
        {"name": "劳动者报酬", "id": "2"},
        {"name": "固定资产折旧", "id": "3"},
        {"name": "生产税净值", "id": "4"},
        {"name": "营业余额", "id": "5"}
      ],
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
  components: {left, detailsDiv},

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
  }

}

</style>
