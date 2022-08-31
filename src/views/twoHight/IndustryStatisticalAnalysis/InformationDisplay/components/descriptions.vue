<template>
  <div class="visibleDiv">
    <div class="visibleDivSelect">
      <label style="margin-right: 5px;margin-left: 5px" class="fl">
        <el-date-picker style="width: 240px" v-model="examineTime" type="daterange"
                        start-placeholder="开始日期" end-placeholder="结束日期" value-format="yyyy-MM-dd">
        </el-date-picker>
      </label>
      <label style="margin-right: 5px;margin-left: 5px" class="fl">
        <el-input v-model.trim="enterpriseName" style="width: 150px" maxlength="20" placeholder="请输入企业名称"></el-input>
      </label>
      <label style="margin-right: 5px;margin-left: 5px" class="fl">
        <el-button type="primary" @click="getList" icon="el-icon-search"
                   style="background-color: #3377FF;width: 100px;height: 35px">搜索
        </el-button>
      </label>
    </div>
    <div class="visibleTable">
      <el-table class="tb-edit" :data="tableData"
                :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                border
                ref="moviesTable"
                highlight-current-row style="width: 95%;margin: auto">
        <el-table-column label="" prop="text" align="left"></el-table-column>
        <el-table-column label="同比" prop="tb" align="center"></el-table-column>
        <el-table-column label="环比" prop="hb" align="center"></el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">

export default {
  name: 'List',
  data() {
    return {
      tableData: [
        { 'text': '增加值总总额（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '劳动者报酬（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '固定资产折旧（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '增加值总总额（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '生产税净值（万元）', 'tb': '2%', 'hb': '4%' },
        { 'text': '营业余额（万元）', 'tb': '2%', 'hb': '4%' }
      ],
      enterpriseName: '',
      examineTime: [],
      currentPage: 1,
      startIndex: 0,
      mrPage: 10,
      pageNum: Number,
      countSize: 0
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
    handleSizeChange(val) {
      this.mrPage = val;
      this.startIndex = (this.currentPage - 1) * this.mrPage;
      this.getList()
    },
    handleCurrentChange(val) {
      this.startIndex = (val - 1) * this.mrPage;
      this.getList()
    }
  },
  props: {}
}
</script>
<style lang="scss">
  .el-table {
    th {
      padding: 0 ;
    }
    td {
      padding: 5px ;
    }
  }

</style>
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
  .el-table {
    th {
      padding: 0 ;
    }
   td {
      padding: 0 ;
    }
  }
}

</style>

