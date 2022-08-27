<template>
  <div class="login-container">
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
    <div class="loginMap">
      <img src="./img/map_03.png" alt="">
      <div class="loginDiv">
        <div class="loginDivTitle">
          <div class="loginDivTitleL">
            <div :class="[clickType ?'clickText':'noClickText']" @click="changeClick(clickType)">管理人员登录</div>
          </div>
          <div class="loginDivTitleR">
            <div :class="[clickType ?'noClickText':'clickText']" @click="changeClick(clickType)">企业人员登录</div>
          </div>
        </div>
        <div class="loginDivCenter">
          <div class="login-btn">
            <span v-if="userLogin">密码登录</span>
            <span v-if="iphoneLogin">短信验证码登录</span>
          </div>
          <el-form ref="form" :model="ruleForm" :rules="rules" label-width="50px" >
            <el-form-item prop="username" style="background-color: #FFFFFF;margin-bottom: 10px" v-if="userLogin">
              <i class="el-icon-user" style="font-size: 130%;"></i>
              <el-input v-model.trim="ruleForm.username" style="width: 80%"
                        maxlength="20"
                        placeholder="登录名/手机号/身份证">
              </el-input>
            </el-form-item>
            <el-form-item prop="password" style="background-color: #FFFFFF;margin-bottom: 10px" v-if="userLogin">
              <i class="el-icon-lock" style="font-size: 130%"></i>
              <el-input v-model.trim="ruleForm.password" style="width: 80%"
                        maxlength="20"
                        placeholder="请输入密码">
              </el-input>
            </el-form-item>

            <el-form-item prop="code" style="background-color: #FFFFFF;margin-bottom: 10px" v-if="userLogin">
              <i class="el-icon-key" style="font-size: 130%"></i>
              <el-input v-model.trim="ruleForm.code" style="width: 50%"
                        maxlength="20"
                        placeholder="请输入验证码"></el-input>
               <div class="yzm">
                 9311
               </div>
            </el-form-item>
            <el-form-item prop="iphone" style="background-color: #FFFFFF;margin-bottom: 10px" v-if="iphoneLogin">
              <i class="el-icon-user" style="font-size: 130%;"></i>
              <el-input v-model.trim="ruleForm.iphone" style="width: 80%"
                        maxlength="20"
                        placeholder="手机号">
              </el-input>
            </el-form-item>
            <el-form-item prop="iphoneCode" style="background-color: #FFFFFF;margin-bottom: 10px" v-if="iphoneLogin">
              <i class="el-icon-key" style="font-size: 130%"></i>
              <el-input v-model.trim="ruleForm.iphoneCode" style="width: 50%"
                        maxlength="20"
                        placeholder="请输入6位短信验证码"></el-input>
              <div class="sedyzm">
               发送验证码
              </div>
            </el-form-item>
            <el-form-item prop="code" style="background-color: #FFFFFF;margin-bottom: 10px">
              <span  style="float: left;cursor: pointer">其他证件登录></span>
              <span  style="float: right;cursor: pointer">忘记密码？</span>
            </el-form-item>
          </el-form>
          <div class="login-btn">
            <el-button type="primary" @click="submitForm('ruleForm')" style="width: 300px">登录</el-button>
            <div class="login-btn-change">
              <div class="" @click="goCodeScanning">扫码登录</div>
              <div class="" @click="goUserLogin">密码登录</div>
            </div>
          </div>
        </div>
        <div class="loginDivBottom">
          <div>还没有账号？</div>
          <div class="goRegister" @click="goRegister">去注册</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {validUsername} from '@/utils/validate'

export default {
  name: 'Login',
  components: {},
  data() {
    return {
      ruleForm: {
        username: "",
        password: "",
        code: "",
        iphone:"",
        iphoneCode:""
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 1, max: 20, message: '用户名在 1 到 20 个字符' }
        ],
        iphone: [
          { required: true, message: '请输手机号', trigger: 'blur' },
          { min: 11, max: 11, message: '手机号在 11 到 11 个字符' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 1, max: 20, message: '密码在 1 到 16 个字符' }
        ],
        iphoneCode: [
          { required: true, message: '请输入验证码', trigger: 'blur' },
          { min: 6, max: 6, message: '验证码在6个字符' }
        ],
        code: [
          { required: true, message: '请输入验证码', trigger: 'blur' },
          { min: 6, max: 6, message: '验证码6 个字符' }
        ]
      },
      passwordType: 'password',
      capsTooltip: false,
      loading: false,
      showDialog: false,
      redirect: undefined,
      otherQuery: {},
      clickType: true,
      iphoneLogin: true,
      adminLogin: false,
      enterpriseLogin: false,
      userLogin: false
    }
  },
  watch: {
    $route: {
      handler: function (route) {
        const query = route.query
        if (query) {
          this.redirect = query.redirect
          this.otherQuery = this.getOtherQuery(query)
        }
      },
      immediate: true
    }
  },
  created() {
  },
  mounted() {
    if (this.loginForm.username === '') {
      this.$refs.username.focus()
    } else if (this.loginForm.password === '') {
      this.$refs.password.focus()
    }
  },
  destroyed() {
    // window.removeEventListener('storage', this.afterQRScan)
  },
  methods: {
    checkCapslock(e) {
      const {key} = e
      this.capsTooltip = key && key.length === 1 && (key >= 'A' && key <= 'Z')
    },
    showPwd() {
      if (this.passwordType === 'password') {
        this.passwordType = ''
      } else {
        this.passwordType = 'password'
      }
      this.$nextTick(() => {
        this.$refs.password.focus()
      })
    },
    handleLogin() {
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          this.loading = true
          this.$store.dispatch('user/login', this.loginForm)
            .then(() => {
              this.$router.push({path: this.redirect || '/', query: this.otherQuery})
              this.loading = false
            })
            .catch(() => {
              this.loading = false
            })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    getOtherQuery(query) {
      return Object.keys(query).reduce((acc, cur) => {
        if (cur !== 'redirect') {
          acc[cur] = query[cur]
        }
        return acc
      }, {})
    },
    changeClick(clickType) {
      this.clickType = !this.clickType
    },
    goRegister() {},
    goCodeScanning() {},
    goUserLogin() {}
  }
}
</script>

<style lang="scss">
/* 修复input 背景不协调 和光标变色 */
/* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

$bg: #283443;
$light_gray: #fff;
$cursor: #fff;

@supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
  .login-container .el-input input {
    color: $cursor;
  }
}

/* reset element-ui css */
.login-container {
  .el-input {
    display: inline-block;
    height: 47px;
    width: 85%;

    input {
      background: transparent;
      border: 0px;
      border-bottom:1px solid #D9E1E7;
      -webkit-appearance: none;
      border-radius: 0px;
      padding: 12px 5px 12px 15px;
      color: #1f2d3d;
      height: 47px;
      caret-color: $cursor;

      &:-webkit-autofill {
        box-shadow: 0 0 0px 1000px $bg inset !important;
        -webkit-text-fill-color: $cursor !important;
      }
    }
  }

  .el-form-item {
    border: 1px solid rgba(255, 255, 255, 0.1);
    background: rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    color: #454545;
  }
  .el-form-item__error{
    left: 25px;
  }
}
</style>

<style lang="scss" scoped>
$bg: #2d3a4b;
$dark_gray: #889aa4;
$light_gray: #eee;

.login-container {
  min-height: 100%;
  width: 100%;
  background-image: url(./img/login.jpg);
  background-size: cover;
  overflow: hidden;

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

  .loginMap {
    width: 100%;
    height: 590px;
    position: absolute;
    left: 0;
    bottom: 0;
    right: 0;
    top: 0;
    margin: auto;

    img {
      margin-left: 272px;
    }

    .loginDiv {
      margin-top: 70px;
      margin-right: 100px;
      width: 400px;
     /* height: 450px;*/
      background: #FFFFFF;
      border-radius: 3px;
      float: right;

    }
  }

  .loginDivTitle {
    height: 80px;

    .loginDivTitleL {
      float: left;
      width: 50%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
    }

    .loginDivTitleR {
      float: left;
      width: 50%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 18px;
      font-weight: bold;
      cursor: pointer;
    }

  }
  .loginDivBottom{
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    .goRegister{
      color: #3377FF;
      cursor: pointer;
    }
  }
  .loginDivCenter{
    width: 100%;
    .yzm{
      float: right;
      width:40%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: flex-start;
      font-size: 20px;
      font-weight: bold;
      color: #3377FF;
    }
    .sedyzm{
      float: right;
      width:40%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content:flex-start;
      font-size: 16px;
      color: #3377FF;
    }
    .login-btn{
      height: 60px;
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      .login-btn-change{
        width: 100%;
        display: flex;
        align-items: center;
        justify-items: flex-start;
        padding-left: 55px;
        margin-top: 10px;
        color: #3377FF;
        div:last-child{
          margin-left: 5px;
          cursor: pointer;
        }
      }
    }
  }
  @media only screen and (max-width: 470px) {
    .thirdparty-button {
      display: none;
    }
  }
}

.clickText {
  color: #3377FF;
  text-decoration: underline;
  text-decoration-color: #3377FF;
  text-decoration-width: 3px;
  text-underline-offset:18px;
}

.noClickText {
  color: #2F3133;
}
</style>
