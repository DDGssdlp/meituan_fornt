<template>
  <div class="page-register">
    <article class="header">
      <header>
        <a href="/" class="site-logo" />
        <span class="login">
          <em class="bold">已有美团账号？</em>
          <a href="/login">
            <el-button type="primary" size="goon">登录</el-button>
          </a>
        </span>
      </header>
    </article>
    <section>
      <div class="headline">
        <span class="headline-content">找回登录密码</span>
      </div>
      <el-steps class="steps" :active="active" style="margin-top: 20px">
        <el-step title="1.确认账号"></el-step>
        <el-step title="2.安全校验"></el-step>
        <el-step title="3.设置密码"></el-step>
        <el-step title="4.完成"></el-step>
      </el-steps>
      <div class="forget-form">
        <div class="op-wrapper">
          <div class="current step-op step-1-op" v-if="active === 1">
            <div class="step-1-title">请填写你要找回密码的美团账号</div>
            <el-input v-model="input.username" size="medium" placeholder="手机号/用户名"></el-input>
            <el-button
              :disabled="flag"
              class="forget-btn"
              @click="handleClick"
              type="success"
              size="goon"
            >下一步</el-button>
          </div>
          <div class="current step-op step-1-op" v-if="active === 2">
            <div class="step-1-title">咱们没有美团的技术 没有安全校验</div>
            <el-image style="width: 300px; height: 100px" :src="url" fit="fill"></el-image>
            <el-button
              :disabled="flag"
              class="forget-btn"
              @click="handleClick"
              type="success"
              size="goon"
            >下一步</el-button>
          </div>
          <div class="current step-op step-1-op" v-if="active === 3">
            <div class="step-1-title">设置密码:</div>
            <el-input v-model="input.password" show-password size="medium" placeholder="新密码"></el-input>
            <el-input
              v-model="input.requirePass"
              show-password
              size="medium"
              placeholder="确认密码"
              style="margin-top: 20px;"
            ></el-input>
            <el-button
              :disabled="flag"
              :plain="true"
              class="forget-btn"
              @click="handleCheck"
              :loading="loading"
              type="success"
              size="goon"
            >下一步</el-button>
          </div>
          <div class="current step-op step-1-op" v-if="active === 4">
            <el-image style="width: 300px; height: auto" :src="url2" fit="fill"></el-image>
            <el-button :disabled="flag" class="forget-btn" @click="toLogin" type="success">进行登录</el-button>
          </div>
        </div>
      </div>
    </section>
    <el-divider></el-divider>

    <p class="copyright" align="center">
      ©
      <a class="f1" href="/">meituan.com</a>&nbsp;
      <a class="f1" target="_blank" href="/">京ICP证070791号</a>&nbsp;
      <span class="f1">京公网安备11010502025545号</span>
    </p>
  </div>
</template>

<script>
//import CryptoJS from 'crypto-js'
import axios from "axios";
export default {
  data() {
    return {
      statusMsg: "",
      error: "",
      loading: false,
      ruleForm: {
        name: "",
        code: "",
        pwd: "",
        cpwd: "",
        email: ""
      },
      url2:
        "https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=1870742492,1611665151&fm=26&gp=0.jpg",
      url:
        "https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2341353904,2363261843&fm=26&gp=0.jpg",
      input: {
        username: "",
        password: ""
      },
      requirePass: "",
      active: 1
    };
  },
  layout: "blank",
  methods: {
    sendMsg: function() {
      const self = this;
      let namePass;
      let emailPass;
      if (self.timerid) {
        return false;
      }
      this.$refs["ruleForm"].validateField("name", valid => {
        namePass = valid;
      });
      self.statusMsg = "";
      if (namePass) {
        return false;
      }
      this.$refs["ruleForm"].validateField("email", valid => {
        emailPass = valid;
      });
      if (!namePass && !emailPass) {
        self.$axios
          .post("/users/verify", {
            //设置中文编码
            username: encodeURIComponent(self.ruleForm.name),
            email: self.ruleForm.email
          })
          .then(({ status, data }) => {
            if (status === 200 && data && data.code === 0) {
              let count = 60;
              self.statusMsg = `验证码已发送,剩余${count--}秒`;
              self.timerid = setInterval(function() {
                self.statusMsg = `验证码已发送,剩余${count--}秒`;
                if (count === 0) {
                  clearInterval(self.timerid);
                  self.timerid = null;
                  self.statusMsg = "";
                }
              }, 1000);
            } else {
              self.statusMsg = data.msg;
            }
          });
      }
    },
    register: function() {
      let self = this;
      this.$refs["ruleForm"].validate(valid => {
        if (valid) {
          self.$axios
            .post("/users/signup", {
              //设置中文编码
              username: window.encodeURIComponent(self.ruleForm.name),
              //使用MD5进行密码加密，MD5处理之后会有很多值，并不是hash值，于是需要toString()函数
              password: CryptoJS.MD5(self.ruleForm.pwd).toString(),
              email: self.ruleForm.email,
              code: self.ruleForm.code
            })
            .then(({ status, data }) => {
              if (status === 200) {
                if (data && data.code === 0) {
                  //强制跳转到登录页面
                  location.href = "/login";
                } else {
                  self.error = data.msg;
                }
              } else {
                self.error = `服务器出错，错误码:${status}`;
              }
              //定时清空error
              setTimeout(function() {
                self.error = "";
              }, 1500);
            });
        }
      });
    },
    handleClick() {
      this.active++;
    },
    handleCheck() {
      this.loading = true;
      if (this.input.password === this.input.requirePass) {
        // 提交密码修改

        this.active++;
      } else {
        this.$message.error("两次输入的密码不一致！");
      }
      this.loading = false;
    },
    toLogin: async function() {
      await this.$axios
        .get(`/product/category/listWithTree`)
        .then(res => {
          this.menu = res.data;
          console.log(res.data);
        })
        .catch(res => {});
    }
  },
  computed: {
    flag: function() {
      // 就是将字符串输入之后才能点击下一页
      return this.input.username.trim() === "";
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/css/forgetpwd/index.scss";
</style>
