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
                :height="300"
                ref="moviesTable"
                highlight-current-row style="width: 98%;margin: auto">
        <el-table-column
          type="selection"
          width="40">
        </el-table-column>
        <el-table-column label="市" prop="jssj" align="center"  width="70"></el-table-column>
        <el-table-column label="区" prop="jssj" align="center"  width="70"></el-table-column>
        <el-table-column label="行业" prop="jssj" align="center"  width="70"></el-table-column>
        <el-table-column label="企业" prop="sdzt" align="center">
          <template slot-scope="scope">
            <el-popover placement="top-start" title="买方主体" width="350" trigger="hover"
                        :content="scope.row.sdzt">
              <div slot="reference"
                   style="width: 100%;height: 100%;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;cursor: pointer">
                {{ scope.row.sdzt }}
              </div>
            </el-popover>
          </template>
        </el-table-column>
        <el-table-column label="烟气量(m³)" prop="kssj" align="center" width="70"></el-table-column>
        <el-table-column label="SO₂(t)" prop="jssj" align="center" width="60"></el-table-column>
        <el-table-column label="NOx(t)" prop="htdl" align="center" width="60"></el-table-column>
        <el-table-column label="PM2.5(t)" prop="lydl" align="center" width="70"></el-table-column>
        <el-table-column label="VOCs(t)" prop="lydl" align="center" width="60"></el-table-column>
      </el-table>
      <div class="handle-page" style="display: flex;align-items: center;justify-content: flex-end;margin-top: 15px;margin-bottom:10px;padding-right: 50px">
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-sizes="[10,50,100, 150,200,250,300]"
          :page-size="mrPage"
          layout="total, sizes, prev, pager, next, jumper"
          :total="countSize">
        </el-pagination>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">

export default {
  name: 'List',
  data() {
    return {
      tableData: [],
      examineTime: '',
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
