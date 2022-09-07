<template>
  <el-dialog title="新增单位" :visible.sync="addDialog" width=40% :close-on-click-modal="false"
             :show-close="true" :close-on-press-escape="false" @close="closeVisible" @open="showAdd">
    <div class="visibleDiv">
      <el-form ref="form" :model="ruleForm" :rules="rules" label-width="170px">
        <el-form-item label="单位名称：" prop="name">
          <el-input v-model.trim="ruleForm.name" style="width: 250px"
                    maxlength="20"
                    placeholder="单位名称"></el-input>
        </el-form-item>
        <el-form-item label="单位类型：" prop="type">
          <el-select style="width: 250px" v-model="ruleForm.type" clearable filterable
                     allow-create default-first-option placeholder="单位类型">
            <el-option
              v-for="item in typeOptions"
              :key="item.id"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="统一社会信用代码：" prop="provinceCode">
          <el-input v-model.trim="ruleForm.code" style="width: 250px"
                    maxlength="20"
                    placeholder="请填写您的单位统一社会信用代码"></el-input>
        </el-form-item>
      </el-form>
      <div
        style="width:100%;height:60px;margin-bottom: 50px;display: flex;align-items: center;justify-content: center">
        <el-button @click="doAdd" type="primary" style="width: 100px;height: 35px;background-color:#3377FF">
          完成
        </el-button>
      </div>
    </div>
  </el-dialog>
</template>

<script type="text/ecmascript-6">



export default {
  name: 'modal',
  data() {
    return {
      ruleForm: {
        name: '',
        type: '',
        code: '',
      },
      rules: {
        name: [
          {required: true, message: '请输入单位名称', trigger: 'blur'},
          {min: 1, max: 20, message: '单位名称在 1 到 20 个字符'}
        ],
        type: [
          {required: true, message: '请输入单位类型', trigger: 'change'}
        ],
        code: [
          {required: true, message: '请输入统一社会信用代码', trigger: 'blur'},
          {min: 1, max: 200, message: '统一社会信用代码在 1 到 200 个字符'},
          {pattern: /^[0-9]*$/, message: '"请输入正确的社会信用代码'}
        ]
      },
      typeOptions: []
    }
  },
  mounted() {


  },
  created() {

  },
  methods: {


    //显示新增
    showAdd() {
      this.ruleForm.name = "";
      this.ruleForm.type = "";
      this.ruleForm.code = "";
      if (this.$refs['form'] !== undefined) {
        this.$nextTick(this.$refs['form'].clearValidate());
      }
    },
    doAdd() {
      this.$refs.form.validate((valid) => {
        if (valid) {
        /*  let that = this;
          const getListData = async () => {
            const result = await greenCardHistory({
              "region": that.region,
              "startTime": that.examineTime[0],
              "endTime": that.examineTime[1]
            })
            that.tableData = result.data.data.data;
          }
          getListData()*/
        } else {
          return this.$message.warning("信息填写不正确");
        }
      })
    },
    closeVisible() {
      this.$emit('closeVisible', 'addDialog')
    },
  },
  props: {
    /**
     * 弹出框
     */
    addDialog: {
      type: Boolean,
      required: true
    }
  },
}
</script>
<style lang="scss" scoped>
.visibleDiv {
  width: 100%;
  height: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

</style>

