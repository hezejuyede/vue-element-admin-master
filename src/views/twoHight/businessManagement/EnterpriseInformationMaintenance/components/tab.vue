<template>
  <div class="tabDiv">
    <div class="tabDivSelect">
      <el-select
        style="width:295px"
        v-model="quota"
        clearable
        filterable
        allow-create
        multiple
        collapse-tags
        default-first-option
        placeholder="行业">
        <el-option
          v-for="item in quotaOptions"
          :key="item.id"
          :label="item.name"
          :value="item.id">
        </el-option>
      </el-select>
    </div>
    <el-tabs v-model="activeName" type="card" @tab-click="handleClick">
      <el-tab-pane label="基本信息">
        <el-table class="tb-edit" :data="tableData"
                  :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                  :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                  border
                  @cell-dblclick="dblclick"
                  highlight-current-row style="width: 95%;margin: auto">
          <el-table-column label="名称项" prop="name1" align="center"></el-table-column>
          <el-table-column label="信息填报项" prop="info1" align="center">
            <template slot-scope="scope">
              <el-input  v-model="scope.row.info1" v-show="scope.row.iseditor" @blur="changeBlur(scope.row.index)"></el-input>
              <span v-show="!scope.row.iseditor">{{scope.row.info1}}</span>
            </template>
          </el-table-column>
          <el-table-column label="名称项" prop="name2" align="center"></el-table-column>
          <el-table-column label="信息填报项" prop="info2" align="center">
            <template slot-scope="scope">
              <el-input  v-model="scope.row.info2" v-show="scope.row.iseditor" @blur="changeBlur(scope.row.index)"></el-input>
              <span v-show="!scope.row.iseditor">{{scope.row.info2}}</span>
            </template>
          </el-table-column>
        </el-table>
      </el-tab-pane>
      <el-tab-pane label="设备信息">
        <div class="visibleDivSelect">
          <label style="margin-right: 5px;margin-left: 5px" class="fl">
            <el-select
              style="width:150px"
              v-model="quota"
              clearable
              filterable
              allow-create
              multiple
              collapse-tags
              default-first-option
              placeholder="行业">
              <el-option
                v-for="item in quotaOptions"
                :key="item.id"
                :label="item.name"
                :value="item.id">
              </el-option>
            </el-select>
          </label>
          <label style="margin-right: 5px;margin-left: 5px" class="fl">
            <el-select
              style="width:150px"
              v-model="status"
              clearable
              filterable
              allow-create
              multiple
              collapse-tags
              default-first-option
              placeholder="装置">
              <el-option
                v-for="item in  statusOptions"
                :key="item.id"
                :label="item.name"
                :value="item.id">
              </el-option>
            </el-select>
          </label>
          <label style="margin-right: 5px;margin-left: 5px" class="fl">
            <el-select
              style="width:150px"
              v-model="status"
              clearable
              filterable
              allow-create
              multiple
              collapse-tags
              default-first-option
              placeholder="设备">
              <el-option
                v-for="item in  statusOptions"
                :key="item.id"
                :label="item.name"
                :value="item.id">
              </el-option>
            </el-select>
          </label>
          <label style="margin-right: 5px;margin-left: 5px" class="fl">
            <el-input v-model.trim="name" style="width: 150px" maxlength="20" placeholder="输入要搜索的内容"></el-input>
          </label>
          <label style="margin-right: 50px;margin-left: 5px" class="fl">
            <el-button type="primary" @click="getList" icon="el-icon-search"
                       style="background-color: #3377FF;width: 100px;height: 35px">搜索
            </el-button>
            <el-button type="primary" @click="getList" icon="el-icon-plus"
                       style="background-color: #3377FF;width: 100px;height: 35px">新增
            </el-button>
            <el-button @click="getList" icon="el-icon-delete"
                       style="border: 1px solid #D8D8D8;width: 100px;color:#959699; height: 35px">删除
            </el-button>
            <el-button @click="getList" icon="el-icon-download"
                       style="border: 1px solid #D8D8D8;width: 100px;color:#959699; height: 35px">导出
            </el-button>
          </label>
        </div>
        <div class="visibleTable">
          <el-table class="tb-edit" :data="tableData2"
                    :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                    :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                    border
                    :height="200"
                    ref="moviesTable"
                    highlight-current-row style="width: 95%;margin: auto">
            <el-table-column type="selection" width="40"></el-table-column>
            <el-table-column label="装置名称" prop="sdzt" align="center"></el-table-column>
            <el-table-column label="设备名称" prop="kssj" align="center"></el-table-column>
            <el-table-column label="规格X数量" prop="jssj" align="center"></el-table-column>
            <el-table-column label="产能" prop="htdl" align="center"></el-table-column>
            <el-table-column label="操作" prop="lydl" align="center" width="100" >
              <template slot-scope="scope">
                <span>删除</span>
              </template>
            </el-table-column>
          </el-table>
          <div class="handle-page"
               style="display: flex;align-items: center;justify-content: flex-end;margin-top: 15px;margin-bottom:10px;padding-right: 50px">
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
      </el-tab-pane>
      <el-tab-pane label="数据填报">
        <div class="visibleDivSelect">
          <label style="margin-right: 50px;margin-left: 5px" class="fl">
            <el-button type="primary" @click="getList" icon="el-icon-plus"
                       style="background-color: #3377FF;width: 100px;height: 35px">新增
            </el-button>
            <el-button @click="getList" icon="el-icon-delete"
                       style="border: 1px solid #D8D8D8;width: 100px;color:#959699; height: 35px">删除
            </el-button>
            <el-button @click="getList" icon="el-icon-download"
                       style="border: 1px solid #D8D8D8;width: 100px;color:#959699; height: 35px">导出
            </el-button>
          </label>
        </div>
        <div class="visibleTable">
          <div class="visibleTableT">
            <el-table class="tb-edit" :data="tableData3"
                      :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                      :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                      border
                      :height="200"
                      ref="moviesTable"
                      highlight-current-row style="width: 95%;margin: auto">
              <el-table-column label="参数" prop="sdzt" align="center" width="150"></el-table-column>
              <el-table-column label="数据填报项" prop="kssj" align="center"></el-table-column>
              <el-table-column label="单位" prop="jssj" align="center"></el-table-column>
            </el-table>
          </div>
          <div class="visibleTableT">
            <el-table class="tb-edit" :data="tableData4"
                      :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                      :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                      border
                      :height="200"
                      ref="moviesTable"
                      highlight-current-row style="width: 95%;margin: auto">
              <el-table-column label="参数" prop="sdzt" align="center" width="150"></el-table-column>
              <el-table-column label="数据填报项" prop="kssj" align="center"></el-table-column>
              <el-table-column label="单位" prop="jssj" align="center"></el-table-column>
            </el-table>
          </div>
          <div class="visibleTableT">
            <el-table class="tb-edit" :data="tableData5"
                      :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                      :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                      border
                      :height="200"
                      ref="moviesTable"
                      highlight-current-row style="width: 95%;margin: auto">
              <el-table-column label="参数" prop="sdzt" align="center" width="150"></el-table-column>
              <el-table-column label="数据填报项" prop="kssj" align="center"></el-table-column>
              <el-table-column label="单位" prop="jssj" align="center"></el-table-column>
            </el-table>
          </div>
        </div>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>
<script type="text/ecmascript-6">

export default {
  name: 'List',
  data() {
    return {
      name: '',
      activeName: '',
      tableData: [
        {'name1': '企业名称', 'info1': '1', 'name2': '统一社会信用代码', 'info2': '9', 'iseditor': false, 'index': '1' },
        {'name1': '所属地市', 'info1': '2', 'name2': '所属区县', 'info2': '10', 'iseditor': false, 'index': '2' },
        {'name1': '企业地址(精确到门牌号)', 'info1': '3', 'name2': '占地面积:(亩)', 'info2': '11', 'iseditor': false, 'index': '3' },
        {'name1': '地理位置:(经度)', 'info1': '4', 'name2': '地理位置:(维度)', 'info2': '12', 'iseditor': false, 'index': '4' },
        {'name1': '行业归属', 'info1': '5', 'name2': '所属性质', 'info2': '13', 'iseditor': false, 'index': '5' },
        {'name1': '法定代表人', 'info1': '6', 'name2': '实际控制人', 'info2': '14', 'iseditor': false, 'index': '6' },
        {'name1': '营业状态', 'info1': '7', 'name2': '是否然煤', 'info2': '15', 'iseditor': false, 'index': '7' },
        {'name1': '是否纳统企业', 'info1': '8', 'name2': '是否规上企业', 'info2': '16', 'iseditor': false, 'index': '8' }
      ],
      tableData2: [],
      tableData3:[],
      tableData4:[],
      tableData5:[],
      quota: "",
      quotaOptions: [],
      status: "",
      statusOptions: [],
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
    handleClick() {
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
    dblclick(row, column, cell, event) {
      if (column.property === 'info1' || column.property === 'info2') {
        for (let i = 0; i < this.tableData.length; i++) {
          if (row.index === this.tableData[i].index) {
            this.tableData[i].iseditor = true
          }
        }
      }
    },
    changeBlur(index) {

      for (let i = 0; i < this.tableData.length; i++) {
        if (index === this.tableData[i].index) {
          this.tableData[i].iseditor = false
        }
      }
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
    padding: 3px;
  }
}

</style>
<style lang="scss" scoped>
.visibleDivSelect {
  height: 80px;
  background-color: #ffffff;
  line-height: 80px;
  padding-left: 2.5%;
}
.visibleTable {
  height: 250px;
}
.tabDivSelect{
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.visibleTableT{
  float: left;
  width: 33%;
  height: 100%;
}
</style>
