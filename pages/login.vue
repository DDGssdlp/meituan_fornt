<template>
  <div class="page-login">
    <div class="login-header">
      <a href="/" class="logo" />
    </div>
    <div class="login-panel">
      <div class="banner">
        <img
          src="//s0.meituan.net/bs/file/?f=fe-sso-fs:build/page/static/banner/www.jpg"
          width="480"
          height="370"
          alt="美团网"
        />
      </div>
      <div class="form">
        <h4 v-if="error" class="tips">
          <i />
          {{ error }}
        </h4>
        <p>
          <span>账号登录</span>
          <span style="float: right">
            <el-link target="_blank" :underline="false" @click="changeLoginWay">
              {{codeLogin}}
              <i class="el-icon-mobile-phone el-icon--right"></i>
            </el-link>
          </span>
        </p>
        <el-input v-model="username" placeholder="请输入用户名/手机号" prefix-icon="profile" />
        <el-input
          v-if="passwordLogin"
          v-model="password"
          
          placeholder="请输入密码"
          prefix-icon="password"
          type="password"
        />
        <el-input
          v-else
          placeholder="请输入验证码"
          maxlength="6"
          show-word-limit
          v-model="phoneCode"
          prefix-icon="password"
        >
          <el-button slot="append" @click="getCheckCode" :disabled="btnChangeEnable">{{msg}}</el-button>
        </el-input>
        <div class="foot">
          <el-checkbox v-model="checked">7天内自动登录</el-checkbox>
          <b class="forget-pwd">
            <el-link type="warning" href="/forgetpwd" :underline="false">忘记密码？</el-link>
          </b>
        </div>
        <el-button class="btn-login" type="success" size="mini" @click="login">登录</el-button>

        <div class="signup-guide">
          <p>
            还没有账号？
            <a href="/register" target="_top">免费注册</a>
          </p>
        </div>
        <div>
          <el-divider content-position="center">
            <font color="#2db3a6" face="微软雅黑">第三方登录</font>
          </el-divider>
          <div>
            <span
              class="oauth__link"
              data-href="/account/connect/tencent"
              target="_blank"
              id="J-third-tencent"
              @click="qqLogin"
            ></span>
            <span
              class="oauth__link2"
              data-href="/account/connect/sina"
              target="_blank"
              id="J-third-sina"
            ></span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
//import CryptoJS from 'crypto-js'
export default {
  data: () => {
    return {
      checked: "",
      codeLogin: "手机动态码登录",
      username: "",
      password: "",
      phoneCode: "",
      error: "",
      btnChangeEnable: false,
      passwordLogin: true,
      msg: "获取验证码",
      num: 60,
      value: 10
    };
  },
  layout: "blank",
  mounted() {},
  methods: {
    // qqLogin
    qqLogin: function() {
      var qqAppId = "101887062"; // 上面申请得到的appid
      var qqAuthPath = "http://www.meituanvue.com:88/api/auth/qq/success"; // 前面设置的回调地址
      var state = "fjdslfjsdlkfd"; // 防止CSRF攻击的随机参数，必传，登录成功之后会回传，最好后台自己生成然后校验合法性
      this.openWindow(
        `https://graph.qq.com/oauth2.0/authorize?response_type=code&client_id=${qqAppId}&redirect_uri=${encodeURIComponent(
          qqAuthPath
        )}&state=${state}`
      );
    },
    // 封装打开页面的方法：
    openWindow: function(url, width, height) {
      width = width || 600;
      height = height || 400;
      var left = (window.screen.width - width) / 2;
      var top = (window.screen.height - height) / 2;
      window.open(
        url,
        "_blank",
        "toolbar=yes, location=yes, directories=no, status=no, menubar=yes, scrollbars=yes, resizable=no, copyhistory=yes, left=" +
          left +
          ", top=" +
          top +
          ", width=" +
          width +
          ", height=" +
          height
      );
    },
    changWord() {
      this.msg = `剩余 ${this.value}秒`;
      --this.value;
      if (this.value < 10) {
        this.msg = `剩余 0${this.value}秒`;
      }

      if (this.value < 0) {
        this.btnChangeEnable = false;
        clearInterval(window.timer);
        this.msg = "获取验证码";
        this.value = 10;
      }
    },
    getCheckCode: async function() {
      if (this.username) {
        this.btnChangeEnable = true;
        window.timer = setInterval(this.changWord, 1000);
        await this.$axios
          .get(`/auth/send/code/${this.username}`)
          .then(res => {
            console.log("code", res);
            if (res.data.isSend) {
              this.$message({
                showClose: true,
                message: "短信验证码发送成功",
                type: "success"
              });
            } else {
              this.$message({
                showClose: true,
                message: `短信验证码发送失败 请稍后再试！`,
                type: "error"
              });
            }
          })
          .catch(err => {});
      } else {
        this.$message({
          showClose: true,
          message: `请输入 手机号！`,
          type: "error"
        });
      }
    },
    changeLoginWay() {
      if(this.passwordLogin){
         this.codeLogin = "账号密码登录"
      }else{
         this.codeLogin = "手机验证码登录"
         
      }
      this.passwordLogin = !this.passwordLogin;
      this.password = "";
      this.phoneCode = "";
    },
    handleClick() {
      // 社交登录功能

      this.$axios.get("/auth/login").then(res => {
        console.log("data", res.data);
        if (res) {
          this.openWindow(res);
        } else {
          this.$message({
            showClose: true,
            message: "登录失败 请重试",
            type: "error"
          });
        }
      });

      //this.$router.push("/");
      //window.location.href = "/";
    },
    login: function() {
      this.$axios
        .post("/auth/login", {
          userName: this.username,
          phoneCode: this.phoneCode,
          password: this.password
        })
        .then(res => {
          console.log("data", res.data);
          if (res.data.code === 0 && res.data.login) {
            localStorage.setItem("loginUser", this.username)
            this.$router.push("/");
          } else if (res.data.code === 500) {
            this.$message({
              showClose: true,
              message: "手机号没有被注册",
              type: "error"
            });
          } else {
            this.$message({
              showClose: true,
              message: "登录失败 请重试",
              type: "error"
            });
          }
        })
        .catch(err => {
          this.$message({
            showClose: true,
            message: "登录失败 请重试！",
            type: "error"
          });
        });
    }
  },
  beforeDestroy() {},
  destory() {
    clearInterval(window.timer);
  }
};
</script>

<style lang="scss">
@import "@/assets/css/login/index.scss";
</style>
