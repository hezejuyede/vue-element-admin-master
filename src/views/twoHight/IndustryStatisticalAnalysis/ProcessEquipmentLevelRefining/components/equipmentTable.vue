<template>
  <div class="visibleDiv">
    <div class="visibleTable">
      <el-table class="tb-edit" :data="tableData"
                :header-cell-style="{background:'#F4F5F9',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4',fontWeight: 'bold'}"
                border
                ref="moviesTable"
                highlight-current-row style="width: 95%;margin: auto">>
        <el-table-column label="装置名称" prop="xx1" align="center"></el-table-column>
        <el-table-column label="型号" prop="value1" align="center"></el-table-column>
        <el-table-column label="数量" prop="xx2" align="center"></el-table-column>
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
        { 'xx1': '一次性炼油装置', 'value1': '420t', 'xx2': '1' },
        { 'xx1': '摧化裂化装置', 'value1': '-', 'xx2': '2' },
        { 'xx1': '催化重整装置', 'value1': '-', 'xx2': '3' },
        { 'xx1': '加氢裂化装置', 'value1': '260t', 'xx2': '4' },
        { 'xx1': '延迟焦化装置', 'value1': '230t', 'xx2': '5' },
        { 'xx1': '乙烯装置', 'value1': '100t', 'xx2': '6' },
        { 'xx1': 'PX装置', 'value1': '-', 'xx2': '6' },
        { 'xx1': '其他装置', 'value1': '743t', 'xx2': '6' },
        { 'xx1': '其他装置', 'value1': '50t', 'xx2': '6' }
      ]
    }
  },
  mounted() {
    this.getList()
    this.getSpanArr(this.tableData)
  },
  created() {
  },
  methods: {
    getList() {
    }
  },
  props: {}
}
</script>
<style lang="scss">
.el-table {
  th {
    padding: 0;
  }
  td {
    padding: 0;
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

}

</style>
