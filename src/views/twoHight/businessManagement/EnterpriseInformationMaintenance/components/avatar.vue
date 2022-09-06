<template>
  <div class="avatar">
    <div class="avatarL">
      <div class="avatarLL">
        <img src="../img/avatar.png" alt="">
      </div>
      <div class="avatarLR">
        <div class="avatarLRT">
          吕秀才
        </div>
        <div class="avatarLRT">
          <label>
            <img src="../img/renz.png" alt="">
            <span style="color: #FF9B21;margin-left: 5px">已经实名认证</span>
          </label>
        </div>
        <div class="avatarLRT">
          <el-button style="border: 1px solid #E6EEFF;width: 120px;height: 35px">修改密码</el-button>
        </div>
        <div class="avatarLRT">
          <el-button style="background-color: #3377FF; color:#ffffff;width: 120px;height: 35px">新增单位</el-button>
        </div>
      </div>
    </div>
    <div class="avatarR">
      <div class="avatarRT">
        <div class="avatarRTL">登录账号：</div>
        <div class="avatarRTC">吕xx</div>
        <div class="avatarRTR" />
      </div>
      <div class="avatarRT">
        <div class="avatarRTL">手机号：</div>
        <div class="avatarRTC">13987654563</div>
        <div class="avatarRTR">
          <el-button style="border: 1px solid #E6EEFF;width: 100px;height: 20px;padding: 0">修改号码</el-button>
        </div>
      </div>
      <div class="avatarRT">
        <div class="avatarRTL">电子信箱：</div>
        <div class="avatarRTC">212323232@qq.com</div>
        <div class="avatarRTR">
          <el-button style="border: 1px solid #E6EEFF;width: 100px;height: 20px;padding: 0">修改邮箱</el-button>
        </div>
      </div>
      <div class="avatarRT">
        <div class="avatarRTL">身份证号：</div>
        <div class="avatarRTC">371321198001019561</div>
        <div class="avatarRTR" />
      </div>
      <div class="avatarRT">
        <div class="avatarRTL">企业数量：</div>
        <div class="avatarRTC">1</div>
        <div class="avatarRTR" />
      </div>
      <div class="avatarRT">
        <div class="avatarRTL">行业：</div>
        <div class="avatarRTC">2</div>
        <div class="avatarRTR" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Avatar'
}
</script>
<style lang="scss" scoped>

.avatar {
  width: 100%;
  height: 170px;
  .avatarL{
    float: left;
    width: 45%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    .avatarLL{
      flex: 1;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      img{
        width: 90%;
      }
    }
    .avatarLR{
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      .avatarLRT{
        margin-bottom: 5px;
      }

    }
  }
  .avatarR{
    float: left;
    width: 55%;
    height: 100%;
    .avatarRT{
      width: 100%;
      height: 25px;
      margin-bottom: 5px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 12px;
      .avatarRTL{
        flex: 1;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-end;
        margin-right: 5px;
      }
      .avatarRTC{
        flex: 1.5;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-start;
      }
      .avatarRTR{
        flex: 1;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-start;
      }
    }
  }

}

</style>
