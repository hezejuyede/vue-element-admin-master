<template>
  <div class="visibleDiv">
    <div class="visibleDivSelect">
      <label style="margin-right: 5px;margin-left: 5px" class="fl">
        <el-select
          style="width:100px"
          v-model="situation"
          clearable
          filterable
          allow-create
          multiple
          collapse-tags
          default-first-option
          placeholder="行业">
          <el-option
            v-for="item in situationOptions"
            :key="item.id"
            :label="item.name"
            :value="item.id">
          </el-option>
        </el-select>
      </label>
      <label style="margin-right: 5px;margin-left: 5px" class="fl">
        <el-select
          style="width:100px"
          v-model="situation"
          clearable
          filterable
          allow-create
          multiple
          collapse-tags
          default-first-option
          placeholder="地级市">
          <el-option
            v-for="item in situationOptions"
            :key="item.id"
            :label="item.name"
            :value="item.id">
          </el-option>
        </el-select>
      </label>
      <label style="margin-right: 5px;margin-left: 5px" class="fl">
        <el-select
          style="width:100px"
          v-model="quota"
          clearable
          filterable
          allow-create
          multiple
          collapse-tags
          default-first-option
          placeholder="县区">
          <el-option
            v-for="item in quotaOptions"
            :key="item.id"
            :label="item.name"
            :value="item.id">
          </el-option>
        </el-select>
      </label>
      <label style="margin-right: 50px;margin-left: 5px" class="fl">
        <el-button type="primary" @click="getList" icon="el-icon-search"
                   style="background-color: #3377FF;width: 100px;height: 35px">搜索
        </el-button>
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
                highlight-current-row style="width: 95%;margin: auto">
        <el-table-column label="" prop="htbh" align="center">
          <template slot-scope="scope">
            <el-popover placement="top-start" title="合同编号" width="350" trigger="hover"
                        :content="scope.row.htbh">
              <div slot="reference"
                   style="width: 100%;height: 100%;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;cursor: pointer">
                {{ scope.row.htbh }}
              </div>
            </el-popover>
          </template>
        </el-table-column>
        <el-table-column label="买方主体" prop="sdzt" align="center">
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
        <el-table-column label="卖方主体" prop="kssj" align="center">
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
        <el-table-column label="合同结算金额" prop="jssj" align="center"></el-table-column>
        <el-table-column label="合同量" prop="htdl" align="center"></el-table-column>
        <el-table-column label="实际应量" prop="lydl" align="center"></el-table-column>
        <el-table-column label="响应度" prop="lydl" align="center"></el-table-column>
        <el-table-column label="合同开始时间" prop="lydl" align="center"></el-table-column>
        <el-table-column label="合同结束时间" prop="lydl" align="center"></el-table-column>
        <el-table-column label="实际结束时间" prop="lydl" align="center"></el-table-column>
        <el-table-column label="电力市场结算情况" prop="lydl" align="center" width="150"></el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">


export default {
  name: 'modal',
  data() {
    return {
      tableData: [],
      quota: "",
      quotaOptions: [],
      situation: "",
      situationOptions: [],
      examineTime: []
    }
  },
  mounted() {
    this.getList()


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
