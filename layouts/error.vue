<template>
  <div class="layout-error">
    <div class="error-container">
      <img
        class="error-img"
        src="https://s1.meituan.net/bs/fe-web-meituan/2d53095/img/not-found.png"
      />
      <p class="error-word">抱歉，页面暂时无法访问...</p>
      <p class="error-msg">错误信息:{{error.message}}</p>

      <el-button type="goon" round @click="handleClick">返回美团首页</el-button>
    </div>
  </div>
</template>

<script>
import MyHeader from "@/components/public/header/index.vue";
import MyFooter from "@/components/public/footer/index.vue";
export default {
  components: {
    MyHeader,
    MyFooter
  },
  layout: "default",
  props: ["error"],
  methods: {
    handleClick() {
      this.$router.push("/");
    }
  }
};
</script>
<style>
.error-container {
  width: 564px;
  margin: 60px auto;
  text-align: center;
}
.error-container .error-img {
  width: 284px;
  height: 224px;
}
.error-container .error-word {
  margin-top: 20px;
  font-size: 20px;
  color: #333333;
}
.error-msg {
  margin-bottom: 30px;
}
</style>>

