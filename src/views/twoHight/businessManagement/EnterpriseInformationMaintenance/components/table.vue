<template>
  <div class="visibleDiv">
    <div class="visibleDivSelect">
      <label style="margin-right: 20px;margin-left: 5px" class="fr">
        <el-button type="primary" @click="openVisible" icon="el-icon-plus"
                   style="background-color: #3377FF;width: 150px;height: 35px">添加单位用户
        </el-button>
      </label>
    </div>
    <div class="visibleTable">
      <el-table class="tb-edit" :data="tableData"
                :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                border
                highlight-current-row style="width: 95%;margin: auto">
        <el-table-column label="用户名" prop="sdzt" align="center"></el-table-column>
        <el-table-column label="姓名" prop="kssj" align="center"></el-table-column>
        <el-table-column label="手机号" prop="jssj" align="center"></el-table-column>
        <el-table-column label="授权截止日期" prop="htdl" align="center"></el-table-column>
        <el-table-column label="操作" prop="lydl" align="center">
          <template slot-scope="scope">
            <span>删除</span>
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">

export default {
  name: 'List',
  data() {
    return {
      tableData: [],
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
    openVisible() {
      this.$emit('openVisible', 'openDialog')
    }
  },
  props: {}
}
</script>
<style lang="scss" scoped>

.visibleDiv {
  width: 100%;
  background-color: #ffffff;
  .visibleDivSelect {
    height: 50px;
    background-color: #ffffff;
    line-height: 50px;
    padding-left: 25px;
  }

}

</style>
