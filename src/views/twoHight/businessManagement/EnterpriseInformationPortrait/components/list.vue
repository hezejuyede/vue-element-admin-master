<template>
  <div class="visibleDiv">
    <div class="visibleDivSelect">
      <label style="margin-right: 5px;margin-left: 5px" class="fl">
        <el-date-picker style="width: 240px" v-model="examineTime" type="daterange"
                        start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
        </el-date-picker>
      </label>
      <label style="margin-right: 50px;margin-left: 5px" class="fl">
        <el-button @click="getList" icon="el-icon-download"
                   style="border: 1px solid #D8D8D8;width: 100px;color:#959699; height: 35px">导出
        </el-button>
      </label>
    </div>
    <div class="visibleTable">
      <el-table class="tb-edit" :data="tableData"
                :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                border
                :height="200"
                ref="moviesTable"
                highlight-current-row style="width: 95%;margin: auto">>
        <el-table-column label="信息项" prop="jssj" align="center"></el-table-column>
        <el-table-column label="数值" prop="jssj" align="center"></el-table-column>
        <el-table-column label="信息项" prop="jssj" align="center"></el-table-column>
        <el-table-column label="数值" prop="sdzt" align="center"></el-table-column>
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
      examineTime: [],
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
  },
  props: {}
}
</script>
<style lang="scss" scoped>

.visibleDiv {
  width: 100%;
  background-color: #ffffff;
  .visibleDivSelect {
    height: 80px;
    background-color: #ffffff;
    line-height: 80px;
    padding-left: 25px;
  }

  .visibleTable {
    height: 250px;
  }

}

</style>
