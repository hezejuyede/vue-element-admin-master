<template>
  <div class="management-container">
    <div :class="leftState ? 'left-show':'left-hide'">
      <div class="left-show-div" @click="showLeft" v-if="leftState">
        <img src="./img/s-q.png" alt="" class="">
      </div>
      <div class="left-hide-div" @click="showLeft" v-if="!leftState">
        <img src="./img/zh-k.png" alt="" class="">
      </div>
      <left></left>
    </div>
    <div :class="leftState ? 'right-show':'right-hide'">
    </div>
  </div>
</template>

<script>
import left from './common/left'
export default {
  name: 'RegisterDiv',
  data() {
    return {
      examineTime: [],
      leftState: true
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
  components: { left },

  created() {
  },
  mounted() {
  },
  destroyed() {
  },
  methods: {
    showLeft() {
      this.leftState = !this.leftState
    }
  }
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
  .left-hide{
    width: 20%;
    position: relative;
    left: -18%;
    top: 0;
    height: 800px;
    transition: all 0.5s;
    z-index: 99;
  }
  .left-show{
    width: 20%;
    height: 800px;
    position: relative;
    left: 0;
    top: 0;
    transition: all 0.5s;
    z-index: 99;
    display: flex;
    align-items: flex-start;
    justify-content: center;

  }
  .left-show-div{
    width: 30px;
    height:100%;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: auto;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    transition: all 0.5s;
    background-color: #C6D6F5;
  }
  .left-hide-div{
    width: 30px;
    height:100%;
    background-color: #C6D6F5;
    position: absolute;
    top: 0;
    left: auto;
    bottom: 0;
    right: 0;
    margin: auto;
    display: flex;
    align-items: center;
    justify-content:flex-end;
    transition: all 0.5s;
  }
  .right-show{
    position: absolute;
    width: 80%;
    left: 20%;
    top:20px;
    height: 800px;
    transition: all 0.5s;
    background-color: #3b91b6;
  }
  .right-hide{
    position: absolute;
    width: 100%;
    left: 0;
    top:20px;
    height: 800px;
    transition: all 0.5s;
    background-color: #3b91b6;
  }

}

</style>
