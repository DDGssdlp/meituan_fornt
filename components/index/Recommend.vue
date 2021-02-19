<template>
  <div class="recommend">
    <div class="high">
      <el-carousel :interval="2000" type="card" height="200px">
        <el-carousel-item v-for="item in images" :key="item.id">
           <el-image class="recommend_image"
          :src="item.idView"
          fit="fill"></el-image>
          <!-- <img :src="item.idView" class="image" /> -->
        </el-carousel-item>
      </el-carousel>
    </div>
    <div></div>
  </div>
</template>

<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';

export default {
  //import引入的组件需要注入到对象中才能使用
  components: {},
  data() {
    //这里存放数据
    return {
      images: [
        { id: 0, idView: "https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=673795924,859869590&fm=26&gp=0.jpg" },
        { id: 1, idView: "https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=673795924,859869590&fm=26&gp=0.jpg" },
        { id: 2, idView: "https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=673795924,859869590&fm=26&gp=0.jpg" }
      ]
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //方法集合
  methods: {},
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {},
  beforeCreate() {}, //生命周期 - 创建之前
  beforeMount() {}, //生命周期 - 挂载之前
  beforeUpdate() {}, //生命周期 - 更新之前
  updated() {}, //生命周期 - 更新之后
  beforeDestroy() {}, //生命周期 - 销毁之前
  destroyed() {}, //生命周期 - 销毁完成
  activated() {} //如果页面有keep-alive缓存功能，这个函数会触发
};
</script>
<style lang="scss">
  @import "@/assets/css/index/recommend.scss";
</style>