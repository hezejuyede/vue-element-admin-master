<template>
  <div class="visibleDiv">
    <div class="visibleDivSelect">
      <label style="margin-right: 5px;margin-left: 5px" class="fl">
        <el-input v-model.trim="enterpriseName" style="width: 300px" maxlength="20" placeholder="企业名称"></el-input>
      </label>
      <label style="margin-right: 50px;margin-left: 5px" class="fl">
        <el-button type="primary" @click="getList" icon="el-icon-search" style="background-color: #3377FF;width: 100px;height: 35px">搜索</el-button>
        <el-button @click="getList" icon="el-icon-download" style="border: 1px solid #D8D8D8;width: 100px;color:#959699; height: 35px">导出</el-button>
      </label>
    </div>
    <div class="visibleTable">
      <el-table class="tb-edit" :data="tableData"
                :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                border
                :height="600"
                ref="moviesTable"
                highlight-current-row style="width: 95%;margin: auto">
        <el-table-column
          type="selection"
          width="40">
        </el-table-column>
        <el-table-column label="用户名称" prop="sdzt" align="center" width="100"  >
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
        <el-table-column label="修改项目" prop="kssj" align="center">
          <template slot-scope="scope">
            <el-popover placement="top-start" title="卖方主体" width="350" trigger="hover"
                        :content="scope.row.kssj">
              <div slot="reference"
                   style="width: 100%;height: 100%;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;cursor: pointer">
                {{ scope.row.kssj }}
              </div>
            </el-popover>
          </template>
        </el-table-column>
        <el-table-column label="资料预览" prop="lydl" align="center"></el-table-column>
        <el-table-column label="提交时间" prop="lydl" align="center"></el-table-column>
        <el-table-column label="意见" prop="lydl" align="center" ></el-table-column>
        <el-table-column label="备注" prop="lydl" align="center"></el-table-column>
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
  name: 'modal1',
  data() {
    return {
      tableData: [],
      enterpriseName: '',
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
    padding-left: 20px;
  }

  .visibleTable {
    height: 290px;

  }

}

</style>
