<template>
  <div class="management-container">
    <div class="containerLeft">
      <div class="containerLeftTop">
        <div class="managementTitle">
          <div class="managementTitleL">
            <div class="">
              <img src="./img/titleImg.png" alt="">
            </div>
            <div class="">
              新增企业
            </div>
          </div>
          <div class="managementTitleR">
            <div class="">
              <el-badge :value="12" class="item">
                <span>代办项</span>
              </el-badge>
            </div>
            <div class="">
              <el-badge :value="3" class="item">
                <span>已办项</span>
              </el-badge>
            </div>
          </div>
        </div>
        <div class="">
          <add></add>
        </div>
      </div>
      <div class="containerLeftBottom">
        <div class="managementTitle">
          <div class="managementTitleL">
            <div class="">
              <img src="./img/titleImg.png" alt="">
            </div>
            <div class="">
              统计分析
            </div>
          </div>
          <div class="managementTitleR">
            <el-date-picker style="width: 250px" v-model="examineTime" type="daterange"
                            start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
            </el-date-picker>
          </div>
        </div>
        <div class="">
          <bar></bar>
        </div>
      </div>
    </div>
    <div class="containerRight">
      <div class="managementTitle">
        <div class="managementTitleL">
          <div class="">
            <img src="./img/titleImg.png" alt="">
          </div>
          <div class="">
           企业资料修改
          </div>
        </div>
        <div class="managementTitleR">
          <div class="">
            <el-badge :value="12" class="item">
              <span>代办项</span>
            </el-badge>
          </div>
          <div class="">
            <el-badge :value="3" class="item">
              <span>已办项</span>
            </el-badge>
          </div>
        </div>
      </div>
      <div class="">
        <edit></edit>
      </div>
    </div>
  </div>
</template>

<script>
import add from './components/add'
import bar from './components/bar'
import edit from './components/edit'
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
  components: { add, bar, edit },

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
  height: 750px;
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

  .containerLeft {
    float: left;
    width: 49%;
    height: 700px;
    background-color: #F8F8F8;
    margin-left: 1%;
    .containerLeftTop{
      height: 340px;
      width: 100%;
      margin-bottom: 20px;
      background-color: #FFFFFF;
    }
    .containerLeftBottom{
      height: 340px;
      width: 100%;
      background-color: #FFFFFF;
    }
  }

  .containerRight {
    float: right;
    width: 49%;
    height: 700px;
    margin-left: 1%;
    background-color: #FFFFFF;
  }
}

</style>
