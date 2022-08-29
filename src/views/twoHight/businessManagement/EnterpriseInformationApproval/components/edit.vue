<template>
    <div class="visibleDiv">
        <div class="visibleTable">
            <el-table class="tb-edit" :data="tableData"
                      :header-cell-style="{background:'#EDF4F4',color:'#474F4F',height:'40px',borderColor:'#CAE5E4',fontSize:'14px',fontWeight: 'bold'}"
                      :cell-style="{fontSize:'12px',fontWeight: 'norma',color:'#444B4B',background:'#FFFFFF',borderColor:'#CAE5E4'}"
                      border
                      :height="320"
                      ref="moviesTable"
                      highlight-current-row style="width: 95%;margin: auto">
                <el-table-column label="单元体名称" prop="htbh" align="center"  width="100">
                    <template slot-scope="scope">
                        <el-popover placement="top-start" title="买方主体" width="350" trigger="hover"
                                    :content="scope.row.htbh">
                            <div slot="reference"
                                 style="width: 100%;height: 100%;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;cursor: pointer">
                                {{ scope.row.htbh }}
                            </div>
                        </el-popover>
                    </template>
                </el-table-column>
                <el-table-column label="单个体" prop=dgt" align="center"></el-table-column>
                <el-table-column label="合同占比" prop="htzb" align="center"></el-table-column>
                <el-table-column label="合同响应度" prop="htxyd" align="center"  width="100"></el-table-column>
                <el-table-column label="计划分配占比" prop="jhfpzb" align="center" width="120"></el-table-column>
                <el-table-column label="实际占比" prop="sjzb" align="center"></el-table-column>
                <el-table-column label="分配额度" prop="fped" align="center" width="100"></el-table-column>
                <el-table-column label="补贴" prop="bt" align="center"></el-table-column>
                <el-table-column label="总计" prop="zj" align="center"  width="100"></el-table-column>
            </el-table>
        </div>
    </div>
</template>

<script type="text/ecmascript-6">
import { ContractPerformance} from "../../../../api/GreenPowerTransactionAggregationAgent/TransactionContractFeedback";

export default {
    name: 'modal',
    data() {
        return {
            tableData:  [],
        }
    },
    mounted() {
        this.getList()


    },
    created() {



    },
    methods: {

        //查询
        getList() {
            let that = this;
            const getListData = async () => {
                const result = await ContractPerformance({})
                  that.tableData = result.data.data.data;

            }
            getListData();

        },
    },

    props: {
    },
}
</script>
<style scoped lang="less" rel="stylesheet/less">


.visibleDiv {
    width: 100%;
    background-color: #ffffff;
    .visibleDivSelect {
        height: 80px;
        background-color: #ffffff;
        line-height: 80px;
    }

    .visibleTable {
        height: 350px;

    }

}

</style>
