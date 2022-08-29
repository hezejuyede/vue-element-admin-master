<template>
  <div class="register-container">
    <div class="loginTitle">
      <div class="loginTitleL">
        <div class="loginTitleL1">山东省 “两高” 行业电子监管平台</div>
        <div class="loginTitleL2"></div>
        <div class="loginTitleL3">用户通行证</div>
      </div>
      <div class="loginTitleR">
        <div class="loginTitleRText">使用帮助</div>
      </div>
    </div>
    <div class="registerText">
      <div class="registerText1">
        <img src="./img/zhuc_03.png" alt="">
      </div>
      <div class="registerText2">
        <div class=""></div>
      </div>
      <div class="registerText3">
        <div class=""><span>1.注册法人账号时需要通过爱山东APP扫脸，请提前做好准备。</span></div>
        <div class=""><span> 2.法人账号注册的相关问题，请查看</span><span style="color: #3A71A8">帮助文档</span><span>。</span></div>
      </div>
    </div>
    <div class="registerTitle">
      <div class="">
        企业人员注册
      </div>
      <div class="">
        <img src="./img/zhuc_07.png" alt="">
      </div>
    </div>
    <div class="registerStep">
      <el-steps :active="step" align-center>
        <el-step title="企业人员认证"></el-step>
        <el-step title="实人认证"></el-step>
        <el-step title="填写单位信息"></el-step>
        <el-step title="填写账号信息"></el-step>
        <el-step title="完成"></el-step>
      </el-steps>
    </div>
    <div class="step1" v-if="step==='0'">
      <el-form ref="form" :model="ruleForm" :rules="rules" label-width="200px">
        <el-form-item label="企业法定代表人姓名：" prop="username" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.username" style="width: 80%"
                    maxlength="20"
                    placeholder="企业法定代表人姓名">
          </el-input>
        </el-form-item>
        <el-form-item label="证件类型：" prop="documentType" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.documentType" style="width: 80%"
                    maxlength="20"
                    :disabled="true"
                    placeholder="证件类型">
          </el-input>
        </el-form-item>
        <el-form-item label="证件号码：" prop="identificationNumber" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.identificationNumber" style="width: 80%"
                    maxlength="20"
                    placeholder="证件号码">
          </el-input>
        </el-form-item>
        <el-form-item label="图形验证码：" prop="code" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.code" style="width: 50%"
                    maxlength="20"
                    placeholder="请输入验证码"></el-input>
          <div class="yzm">
            9311
          </div>
        </el-form-item>
      </el-form>
      <div class="login-btn">
        <div class=""><span>注册有问题？点击这里咨询</span><span style="color: #3A71A8;cursor: pointer">智能客服</span></div>
        <el-button type="primary" @click="nextStep(step)" style="width: 300px;border-radius: 10px">下一步
        </el-button>
      </div>
    </div>
    <div class="step2" v-if="step==='1'">
      <div class="step2Div">
        <div class="titleDiv">
          <div class="titleDivL">
            <img src="./img/zhuc_11.png" alt="">
          </div>
          <div class="titleDivR"  style="font-weight: bold;">
            扫脸认证
          </div>
        </div>
        <div class="step2DivContent">
          <div class="">
            <img src="./img/avatar.png" alt="">
          </div>
          <div class="">
            <div class="" style="">刷脸认证</div>
            <div class="" style="color: #3A71A8;  margin-top: 10px;">使用扫脸方式认证,认证成功后跳转下一步</div>
          </div>
          <div class="">
            <el-button type="primary" @click="showSM" style="width: 200px;border-radius: 10px;background-color: #3377FF">立即认证</el-button>
          </div>
        </div>
      </div>
      <div class="login-step">
        <el-button type="primary" @click="nextStep(step)" style="width: 300px;border-radius: 10px">下一步</el-button>
        <el-button @click="previousStep(step)" style="width: 300px;border-radius: 10px;border: 1px solid #709FFF;color:#709FFF">返回</el-button>
      </div>
    </div>
    <div class="step1" v-if="step==='2'">
      <el-form ref="form" :model="ruleForm" :rules="rules" label-width="200px">
        <el-form-item label="单位名称：" prop="unitName" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.username" style="width: 80%"
                    maxlength="20"
                    placeholder="请输入单位名称">
          </el-input>
        </el-form-item>
        <el-form-item label="单位类型：" prop="unitType" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-select style="width: 80%" v-model="ruleForm.unitType" clearable filterable
                     allow-create default-first-option placeholder="请选择单位类型">
            <el-option
              v-for="item in unitTypeOptions"
              :key="item.id"
              :label="item.name"
              :value="item.id">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="统一社会信用代码：" prop="unifiedSocialCreditCode" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.unifiedSocialCreditCode" style="width: 80%"
                    maxlength="20"
                    placeholder="请输入统一社会信用代码">
          </el-input>
        </el-form-item>
      </el-form>
      <div class="login-step">
        <el-button type="primary" @click="nextStep(step)" style="width: 300px;border-radius: 10px">下一步</el-button>
        <el-button  @click="previousStep(step)" style="width: 300px;border-radius: 10px;border: 1px solid #709FFF;color:#709FFF">返回</el-button>
      </div>
    </div>
    <div class="step1" v-if="step==='3'">
      <el-form ref="form" :model="ruleForm" :rules="rules" label-width="200px">
        <el-form-item label="企业代表人账号：" prop="accountNumber" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.username" style="width: 80%"
                    maxlength="20"
                    placeholder="企业法定代表人姓名">
          </el-input>
        </el-form-item>
        <el-form-item label="密码：" prop="password1" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.password1" style="width: 80%"
                    maxlength="18"
                    placeholder="长度6-18位，建议两种或以上字母，数字，符合组合">
          </el-input>
        </el-form-item>
        <el-form-item label="确认密码：" prop="password2" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.password2" style="width: 80%"
                    maxlength="18"
                    placeholder="请填写确认密码">
          </el-input>
        </el-form-item>
        <el-form-item label="手机号：" prop="phone" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.phone" style="width: 80%"
                    maxlength="11"
                    placeholder="请填写手机号">
          </el-input>
        </el-form-item>
        <el-form-item label="邮箱：" prop="email" style="background-color: #FFFFFF;margin-bottom: 25px">
          <el-input v-model.trim="ruleForm.email" style="width: 80%"
                    maxlength="20"
                    placeholder="请填写邮箱">
          </el-input>
        </el-form-item>
      </el-form>
      <div class="login-step">
        <el-button type="primary" @click="nextStep(step)" style="width: 300px;border-radius: 10px">下一步</el-button>
        <el-button  @click="previousStep(step)" style="width: 300px;border-radius: 10px;border: 1px solid #709FFF;color:#709FFF">返回</el-button>
      </div>
    </div>
    <div class="step1" v-if="step==='4'">
      <div class="titleDiv">
        <div class="titleDivL">
          <img src="./img/zhuc_11.png" alt="">
        </div>
        <div class="titleDivR"  style="font-weight: bold;">
          信息总览
        </div>
      </div>
      <el-form ref="form" :model="ruleForm" label-width="200px"  style="margin-top: 50px">
        <el-form-item label="企业法定代表人姓名：" style="background-color: #FFFFFF;margin-bottom: 5px">
          {{ruleForm.username}}
        </el-form-item>
        <el-form-item label="证件号码：" style="background-color: #FFFFFF;margin-bottom: 5px">
          {{ruleForm.identificationNumber}}
        </el-form-item>
        <el-form-item label="单位名称：" style="background-color: #FFFFFF;margin-bottom: 5px">
          {{ruleForm.unitName}}
        </el-form-item>
        <el-form-item label="单位类型：" style="background-color: #FFFFFF;margin-bottom: 5px">
          {{ruleForm.unitType}}
        </el-form-item>
        <el-form-item label="统一社会信用代码：" style="background-color: #FFFFFF;margin-bottom: 5px">
          {{ruleForm.unifiedSocialCreditCode}}
        </el-form-item>
        <el-form-item label="企业法定代表人账号：" style="background-color: #FFFFFF;margin-bottom: 5px">
          {{ruleForm.accountNumber}}
        </el-form-item>
        <el-form-item label="手机号：" style="background-color: #FFFFFF;margin-bottom: 5px">
          {{ruleForm.phone}}
        </el-form-item>
        <el-form-item label="邮箱：" style="background-color: #FFFFFF;margin-bottom: 5px">
          {{ruleForm.email}}
        </el-form-item>
      </el-form>
      <div class="login-step">
        <el-button type="primary" @click="nextStep(step)" style="width: 300px;border-radius: 10px">确认</el-button>
        <el-button  @click="previousStep(step)" style="width: 300px;border-radius: 10px;border: 1px solid #709FFF;color:#709FFF">返回</el-button>
      </div>
    </div>
    <el-dialog title="扫脸认证" :visible.sync="displayCodeScanning" width="40%" :close-on-click-modal="false"
               :show-close="true" :close-on-press-escape="false">
      <div class="visibleDiv">
        <img src="./img/saomiao.gif" alt="">
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'RegisterDiv',
  components: {},
  data() {
    return {
      step: '0',
      unitTypeOptions: [
        {"name": "炼化", "id": "1"},
        {"name": "焦化", "id": "2"},
        {"name": "煤加工", "id": "3"},
        {"name": "化学原料", "id": "4"},
        {"name": "肥料", "id": "5"},
        {"name": "轮胎", "id": "6"},
        {"name": "水泥", "id": "7"},
        {"name": "石灰", "id": "8"},
        {"name": "防水建材", "id": "9"},
        {"name": "玻璃", "id": "10"},
        {"name": "陶瓷", "id": "11"},
        {"name": "钢铁", "id": "12"},
        {"name": "铁合金", "id": "13"},
        {"name": "有色", "id": "14"},
        {"name": "铸造", "id": "15"},
        {"name": "煤电", "id": "16"},
      ],
      ruleForm: {
        username: '',
        documentType: '身份证',
        identificationNumber: '',
        code: '',
        unitName: '',
        unitType: '',
        unifiedSocialCreditCode: '',
        accountNumber: '',
        password1: '',
        password2: '',
        phone: '',
        email: ''
      },
      rules: {
        username: [
          { required: true, message: '请输入企业法定代表人姓名', trigger: 'blur' },
          { min: 1, max: 20, message: '企业法定代表人姓名在 1 到 20 个字符' }
        ],
        documentType: [
          { required: true, message: '请输证件类型', trigger: 'blur' }
        ],
        identificationNumber: [
          { required: true, message: '请输证件号码', trigger: 'blur' },
          { min: 18, max: 18, message: '证件号码在 18 到 18 个字符' }
        ],
        code: [
          { required: true, message: '请输入验证码', trigger: 'blur' },
          { min: 6, max: 6, message: '验证码6 个字符' }
        ],
        unitName: [
          { required: true, message: '请输入单位名称', trigger: 'blur' },
          { min: 18, max: 18, message: '单位名称在 18 到 18 个字符' }
        ],
        unitType: [
          { required: true, message: '请输入单位类型', trigger: 'change' },
        ],
        unifiedSocialCreditCode: [
          { required: true, message: '请输统一社会信用代码', trigger: 'blur' },
          { min: 18, max: 18, message: '统一社会信用代码在 18 到 18 个字符' }
        ]
        ,
        accountNumber: [
          { required: true, message: '请输入企业代表人账号', trigger: 'blur' },
          { min: 6, max: 6, message: '企业代表人账号6 个字符' }
        ],
        password1: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 18, max: 18, message: '密码在 18 到 18 个字符' }
        ],
        password2: [
          { required: true, message: '请填写确认密码', trigger: 'blur' },
          { min: 18, max: 18, message: '请填写确认密码在 18 到 18 个字符' }
        ],
        phone: [
          { required: true, message: '请填写手机号', trigger: 'blur' },
          { min: 11, max: 11, message: '手机号在 11 到 11 个字符' }
        ],
        email: [
          { required: true, message: '请填写邮箱', trigger: 'blur' },
          { min: 18, max: 18, message: '邮箱在 18 到 18 个字符' }
        ]
      },
      displayCodeScanning: false
    }
  },
  watch: {
    $route: {
      handler: function (route) {
      },
      immediate: true
    }
  },
  created() {
  },
  mounted() {
  },
  destroyed() {
  },
  methods: {
    nextStep(step) {
      if (this.step === '4') {
        this.$message.success('注册完成')
      } else {
        this.step = (parseInt(step) + 1) + ''
      }
    },
    previousStep(step) {
      this.step = (parseInt(step) - 1) + ''
    },
    showSM() {
      this.displayCodeScanning = true
    }
  }
}
</script>
<style lang="scss" scoped>

.register-container {
  .loginTitle {
    width: 100%;
    height: 70px;
    background: #0449AE;

    .loginTitleL {
      float: left;
      width: 60%;
      height: 70px;
      display: flex;
      align-items: center;
      justify-content: center;

      .loginTitleL1 {
        width: 450px;
        height: 70px;
        font-size: 26px;
        font-family: PangMenZhengDao;
        font-weight: 700;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #FFFFFF;
      }

      .loginTitleL2 {
        width: 1px;
        height: 30px;
        border: 1px solid #FFFFFF;
        opacity: 0.5;
      }

      .loginTitleL3 {
        width: 119px;
        height: 70px;
        font-size: 16px;
        font-family: SourceHanSansCN;
        font-weight: 400;
        color: #FFFFFF;
        display: flex;
        align-items: center;
        justify-content: center;
      }
    }

    .loginTitleR {
      float: right;
      width: 40%;
      height: 70px;
      display: flex;
      align-items: center;
      justify-content: flex-start;

      .loginTitleRText {
        width: 96px;
        height: 28px;
        border: 1px solid #F8F8F8;
        opacity: 0.5;
        border-radius: 5px;
        font-size: 16px;
        font-weight: bold;
        color: #FFFFFF;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
      }
    }

  }

  .registerText {
    width: 95%;
    margin: 0 auto;
    height: 80px;
    background: #FDF6EC;

    .registerText1 {
      float: left;
      width: 6%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .registerText2 {
      float: left;
      width: 3%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;

      div {
        width: 1px;
        height: 60px;
        border: 1px solid #0449AE;
        opacity: 0.3;
      }
    }

    .registerText3 {
      float: left;
      width: 84%;
      height: 100%;
      display: flex;
      align-items: flex-start;
      justify-content: center;
      flex-direction: column;
      color: #32343A;

      div:first-child {
        margin-bottom: 10px;
      }

    }
  }

  .registerTitle {
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    font-size: 30px;
    color: #2F3133;
    font-weight: bold;
  }

  .registerStep {
    height: 100px;
    width: 90%;
    margin: 0 auto;
  }

  .step1 {
    width: 60%;
    height: 100%;
    margin: 0 auto;
    font-weight: bold;


  }

  .yzm {
    float: right;
    width: 40%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    font-size: 20px;
    font-weight: bold;
    color: #3377FF;
  }

  .login-btn {
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;

    div {
      margin-bottom: 20px;
    }
  }
  .login-step{
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .titleDiv{
    width: 800px;
    height: 30px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    border-bottom: 1px solid #E0E0E0;
    img{
      margin-right: 5px;
      margin-top:3px;
    }
  }
  .step2DivContent{
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
    div:first-child{
      margin-right: 20px;
    }
    div:nth-child(2){
      margin-right: 50px;
    }
  }
  .visibleDiv{
    width:100%;
    height: 400px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}

</style>
