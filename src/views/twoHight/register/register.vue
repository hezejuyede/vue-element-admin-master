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
      <el-steps :active="0" align-center>
        <el-step title="企业人员认证"></el-step>
        <el-step title="实人认证"></el-step>
        <el-step title="填写单位信息"></el-step>
        <el-step title="填写账号信息"></el-step>
        <el-step title="完成"></el-step>
      </el-steps>
    </div>
    <div class="step1">
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
        <el-button type="primary" @click="submitForm('ruleForm')" style="width: 300px;border-radius: 10px">下一步
        </el-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'registerDiv',
  components: {},
  data() {
    return {
      ruleForm: {
        username: '',
        documentType: '身份证',
        identificationNumber: '',
        code: ''
      },
      rules: {
        username: [
          {required: true, message: '请输入企业法定代表人姓名', trigger: 'blur'},
          {min: 1, max: 20, message: '企业法定代表人姓名在 1 到 20 个字符'}
        ],
        documentType: [
          {required: true, message: '请输证件类型', trigger: 'blur'}
        ],
        identificationNumber: [
          {required: true, message: '请输证件号码', trigger: 'blur'},
          {min: 18, max: 18, message: '证件号码在 18 到 18 个字符'}
        ],
        code: [
          {required: true, message: '请输入验证码', trigger: 'blur'},
          {min: 6, max: 6, message: '验证码6 个字符'}
        ]
      }
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
  methods: {}
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
}

</style>
