<template>
  <div class="visibleDiv">
    <div class="visibleTable">
      <el-table class="tb-edit" :data="tableData"
                :header-cell-style="{background:'#F4F5F9',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4',fontWeight: 'bold'}"
                border
                ref="moviesTable"
                :span-method="objectSpanMethod"
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
        {'xx1': '综合能源消费量', 'value1': '460㎡', 'xx2': '1'},
        {'xx1': '综合能源消费量', 'value1': '510㎡', 'xx2': '2'},
        {'xx1': '综合能源消费量', 'value1': '1080㎡', 'xx2': '3'},
        {'xx1': '综合能源消费量', 'value1': '1880㎡', 'xx2': '4'},
        {'xx1': '综合能源消费量', 'value1': '3200㎡', 'xx2': '5'},
        {'xx1': '综合能源消费量', 'value1': '3800㎡', 'xx2': '6'}
      ],
      examineTime: [],
      spanArr: [],
      pos: ''
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
    },
    getSpanArr(data) {
      // data就是我们从后台拿到的数据
      for (var i = 0; i < data.length; i++) {
        if (i === 0) {
          this.spanArr.push(1)
          this.pos = 0
        } else {
          // 判断当前元素与上一个元素是否相同
          if (data[i].staid === data[i - 1].staid) {
            this.spanArr[this.pos] += 1
            this.spanArr.push(0);
          } else {
            this.spanArr.push(1)
            this.pos = i
          }
        }
      }
    },
    // 合并的方法
    objectSpanMethod({row, column, rowIndex, columnIndex}) {
      if (columnIndex === 0) {
        const _row = this.spanArr[rowIndex]
        const _col = _row > 0 ? 1 : 0
        console.log(`rowspan:${_row} colspan:${_col}`)
        return {
          // [0,0] 表示这一行不显示， [2,1]表示行的合并数
          rowspan: _row,
          colspan: _col
        };
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
