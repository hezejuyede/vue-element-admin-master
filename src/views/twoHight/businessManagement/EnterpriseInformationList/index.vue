<template>
  <div class="management-container">
    <left :leftState="leftState" @showLeft="showRight"></left>
    <div :class="leftState ? 'right-show':'right-hide'">
      <div class="containerTop">
        <div class="containerTopL">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                总览
              </div>
            </div>
            <div class="managementTitleR">
            </div>
          </div>
        </div>
        <div class="containerTopR">
          <div class="managementTitle">
            <div class="managementTitleL">
              <div class="">
                <img src="./img/titleImg.png" alt="">
              </div>
              <div class="">
                济南市企业分布状况
              </div>
            </div>
            <div class="managementTitleR">
            </div>
          </div>
        </div>
      </div>
      <div class="containerBottom">
        <div class="managementTitle">
          <div class="managementTitleL">
            <div class="">
              <img src="./img/titleImg.png" alt="">
            </div>
            <div class="">
                企业清单
            </div>
          </div>
          <div class="managementTitleR">
          </div>
        </div>
        <list-div></list-div>
      </div>
    </div>
  </div>
</template>

<script>
import left from './common/left'
import listDiv from './components/list'

export default {
  name: 'RegisterDiv',
  data() {
    return {
      leftState: true
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
  components: { left, listDiv },

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
  height: 850px;
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
        margin-right: 20px;
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
    width: 100%;
    left: 0;
    top: 20px;
    height: 800px;
    transition: all 0.5s;
  }
  .containerTop{
    height: 380px;
    margin-bottom: 20px;
    .containerTopL{
      width: 49%;
      height: 100%;
      background-color: #ffffff;
      margin-right: 1%;
      float: left;
    }
    .containerTopR{
      width: 49%;
      height: 100%;
      background-color: #ffffff;
      margin-right: 1%;
      float: left;
    }
  }
  .containerBottom{
    height: 400px;
    background-color: #ffffff;
  }
}

</style>
