<template>
  <div class="m-life">
    <el-row>
      <el-col :span="14">
        <slider />
      </el-col>
      <el-col :span="4">
        <div class="m-life-pic" />
      </el-col>
      <el-col :span="6">
        <div class="m-life-login" v-if="!login">
          <h4>
            <img src="//s0.meituan.net/bs/fe-web-meituan/2d05c2b/img/avatar.jpg" alt />
          </h4>
          <p class="m-life-login-name">Hi！你好</p>
          <p>
            <nuxt-link to="/register">
              <el-button round size="medium">注册</el-button>
            </nuxt-link>
          </p>
          <p>
            <nuxt-link to="/login">
              <el-button round size="medium">立即登录</el-button>
            </nuxt-link>
          </p>
        </div>
        <div class="m-life-login" v-else>
          <div class="setting">
            <a href="/settings" target="_blank">
              <div class="icon">
                <i class="el-icon-setting"></i>
              </div>
            </a>
          </div>
          <div class="default" style="display: block;">
            <h4>
              <img src="https://gitee.com/ssdls/blogimg/raw/master/img/20210202165156.jpg" alt />
            </h4>
          </div>
          <p class="login-name">{{user}}</p>
          <div class="menu-list">
            <el-row>
              <el-col :span="8">
                <div class="icon2">
                  <a href="/order" target="_blank">
                    <i class="el-icon-s-order"></i>
                  </a>
                </div>
              </el-col>
              <el-col :span="8">
                <div class="icon2">
                  <a href="/order" target="_blank">
                    <i class="el-icon-star-on"></i>
                  </a>
                </div>
              </el-col>
              <el-col :span="8">
                <div class="icon2">
                  <a href="/order" target="_blank">
                    <i class="el-icon-s-ticket"></i>
                  </a>
                </div>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="8">
                <div class="fn-name">我的订单</div>
              </el-col>
              <el-col :span="8">
                <div class="fn-name">我的收藏</div>
              </el-col>
              <el-col :span="8">
                <div class="fn-name">我的优惠</div>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="8">
                <div class="icon2">
                  <a href="/order" target="_blank">
                    <i class="el-icon-s-finance"></i>
                  </a>
                </div>
              </el-col>
              <el-col :span="8">
                <div class="icon2">
                  <a href="" target="_blank">
                    <i class="el-icon-more"></i>
                  </a>
                </div>
              </el-col>
            </el-row>
            <el-row>
              <el-col :span="8">
                <div class="fn-name-2">余额</div>
              </el-col>
              <el-col :span="8">
                <div class="fn-name-2">更多</div>
              </el-col>
            </el-row>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="7">
        <div class="m-life-hotel" />
      </el-col>
      <el-col :span="7">
        <div class="m-life-music" />
      </el-col>
      <el-col :span="4">
        <div class="m-life-coop" />
      </el-col>
      <el-col :span="6">
        <div class="m-life-downapp">
          <img src="//s1.meituan.net/bs/fe-web-meituan/60ac9a0/img/download-qr.png" alt="下载APP" />
          <p>美团APP手机版</p>
          <h4>
            <span class="red">1元起</span>
            <em class="gary">吃喝玩乐</em>
          </h4>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import Slider from "./slider.vue";
export default {
  data() {
    return {
      login: false,
      user: ""
    };
  },
  components: {
    Slider
  },
  activated() {
    
  },
  async mounted() {
    let loginUserPhone = localStorage.getItem("loginUser");
    if (loginUserPhone) {
      await this.$axios
        .get(`member/member/getLoginUser/${loginUserPhone}`)
        .then(res => {
          if (res.data.loginUser) {
            this.login = true;
            this.user = res.data.loginUser.userName;
          }else{
            localStorage.removeItem("loginUser")
          }
        });
    }
  }
};
</script>


<style lang="scss">
@import "@/assets/css/index/life.scss";
</style>
