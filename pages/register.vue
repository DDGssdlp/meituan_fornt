<template>
  <div class="page-register">
    <article class="header">
      <header>
        <a href="/" class="site-logo" />
        <span class="login">
          <em class="bold">已有美团账号？</em>
          <a href="/login">
            <el-button type="goon" size="small">登录</el-button>
          </a>
        </span>
      </header>
    </article>
    <section>
      <el-form
        ref="ruleForm"
        :model="ruleForm"
        :rules="rules"
        label-width="100px"
        class="demo-ruleForm"
      >
        <el-form-item label="昵称" prop="userName">
          <el-input v-model="ruleForm.name" />
        </el-form-item>
        <el-form-item label="手机号" prop="phoneNum">
          <el-input v-model="ruleForm.phone" />
          <el-button size="mini" :disabled="btnChangeEnable" round @click="sendMsg">{{codemsg}}</el-button>
          <span class="status">{{ statusMsg }}</span>
        </el-form-item>
        <el-form-item label="短信动态码" prop="phoneCode">
          <el-input v-model="ruleForm.code" maxlength="6" show-word-limit />
        </el-form-item>
        <el-form-item label="创建密码" prop="password">
          <el-input show-password v-model="ruleForm.pwd" type="password" />
        </el-form-item>
        <el-form-item label="确认密码" prop="cpwd">
          <el-input show-password v-model="ruleForm.cpwd" type="password" />
        </el-form-item>
        <el-form-item>
          <el-button type="goon" @click="register">同意以下协议并注册</el-button>
          <div class="error">{{ error }}</div>
        </el-form-item>
        <el-form-item>
          <a class="f1" href="http://www.meituan.com/about/terms" target="_blank">《美团用户协议》</a>
          <a
            class="f1"
            href="https://rules-center.meituan.com/rules-detail/2"
            target="_blank"
          >《美团隐私政策》</a>
        </el-form-item>
      </el-form>
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
//import axios from "axios";
export default {
  data() {
    return {
      codemsg: "发送验证码",
      value: 10,
      btnChangeEnable: false,
      statusMsg: "",
      error: "",
      ruleForm: {
        name: "",
        code: "",
        pwd: "",
        cpwd: "",
        phone: ""
      },
      rules: {
        name: [
          {
            required: true,
            type: "string",
            message: "请输入昵称",
            trigger: "blur"
          }
        ],
        phone: [
          {
            required: true,
            message: "请输入正确手机号",
            trigger: "blur"
          }
        ],
        pwd: [
          {
            required: true,
            message: "创建密码",
            trigger: "blur"
          }
        ],
        cpwd: [
          {
            required: true,
            message: "确认密码",
            trigger: "blur"
          },
          {
            validator: (rule, value, callback) => {
              if (value === "") {
                callback(new Error("请再次输入密码"));
              } else if (value !== this.ruleForm.pwd) {
                callback(new Error("两次输入密码不一致"));
              } else {
                callback();
              }
            },
            trigger: "blur"
          }
        ]
      }
    };
  },
  layout: "blank",
  methods: {
    changWord: function() {
      this.codemsg = `${this.value}秒之后再次发送`;
      --this.value;
      if (this.value < 10) {
        this.msg = `剩余 0${this.value}秒`;
      }
      if (this.value < 0) {
        this.btnChangeEnable = false;
        clearInterval(window.timer);
        this.codemsg = "发送验证码";
        this.value = 10;
      }
    },
    sendMsg: async function() {
      this.btnChangeEnable = true;
      window.timer = setInterval(this.changWord, 1000);
      if(this.ruleForm.phone){
        await this.$axios
        .get(`/auth/send/code/${this.ruleForm.phone}`)
        .then(res => {
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
          console.log(res);
        })
        .catch(err => {});
      }else{
        this.$message({
              showClose: true,
              message: `请输入 手机号！`,
              type: "error"
            });
      }
      
    },
    register: function() {

        let datastr = {
          userName: this.ruleForm.name,
          phoneNum: this.ruleForm.phone,
          phoneCode: this.ruleForm.code,
          password: this.ruleForm.pwd
        }
        
        this.$axios.post(`/auth/register`, datastr )
       .then(res => {
          console.log(res)
          if(res.data.code === 0 && res.data.register){
           
            this.$router.push('/login')
          }else if (res.data.code ===40001){
            this.$message({
             showClose: true,
             message: "手机号已经注册！",
             type: 'error' });
          }else{
             this.$message({
             showClose: true,
             message: "验证码失效",
             type: 'error' });
          }
       })
       .catch(err => {
         this.$message({
             showClose: true,
             message: '用户注册失败 请稍后再试！',
             type: 'error' });
       });
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/css/register/index.scss";
</style>
