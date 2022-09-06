<template>
  <div class="management-container">
    <div class="containerTop">
      <div class="managementTitle">
        <div class="managementTitleL">
          <div class="">
            <img src="./img/titleImg.png" alt="">
          </div>
          <div class="">
            信息认证
          </div>
        </div>
        <div class="managementTitleR">
        </div>
      </div>
      <div class="topDiv">
        <div class="topDivL">
          <avatar-div></avatar-div>
        </div>
        <div class="topDivR">
          <table-div></table-div>
        </div>
      </div>
    </div>
    <div class="containerCenter">
      <tab-div></tab-div>
    </div>
    <div class="containerBottom">
      <div class="managementTitle">
        <div class="managementTitleL">
          <div class="">
            <img src="./img/titleImg.png" alt="">
          </div>
          <div class="">
            企业信息修改跟踪
          </div>
        </div>
        <div class="managementTitleR">
        </div>
      </div>
      <div class="containerBottomImg">
        <img src="./img/modifyTracking.png" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import tableDiv from './components/table'
import avatarDiv from './components/avatar'
import tabDiv from './components/tab'
export default {
  name: 'RegisterDiv',
  data() {
    return {
      examineTime: []
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
  components: { tableDiv, avatarDiv, tabDiv },

  created() {
  },
  mounted() {
  },
  destroyed() {
  },
  methods: {}
}
</script>
<style lang="scss">
.el-badge__content.is-fixed {
  right:0
}
</style>
<style lang="scss" scoped>

.management-container {
  width: 100%;
  height: 1000px;
  background-color: #F8F8F8;
  padding-top: 10px;

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
  .containerTop{
    width: 97%;
    height: 250px;
    margin: 15px auto 0 auto;
    background-color: #ffffff;
    .topDiv{
      width: 100%;
      height: 170px;
      .topDivL {
        float: left;
        width: 49%;
        height: 100%;
        border-right: 1px solid #E8E8E8;
      }
      .topDivR {
        float: left;
        width: 50%;
        height: 100%;
      }
    }
  }
  .containerCenter{
    width: 97%;
    height: 500px;
    margin: 15px auto 0 auto;
    background-color: #ffffff;
  }
  .containerBottom{
    width: 97%;
    height: 180px;
    margin: 15px auto 0 auto;
    background-color: #ffffff;
    .containerBottomImg{
      width: 90%;
      margin: 0 auto;
      height: 120px;
      display: flex;
      align-items: center;
      justify-content: center;
      img{
        width: 100%;
      }
    }
  }
}

</style>
