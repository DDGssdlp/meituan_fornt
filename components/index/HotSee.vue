<template>
  <div class="hot_see">
  <el-row :gutter="100" class="hot_cont">
    <el-col :span="2">
       <el-image class="hot_image"
      :src="url"
      fit="fill"></el-image>
  
      </el-col>
    <el-col :span="22">
        <el-image class="hot_image2"
      :src="url2"
      @click="handlerClick"
      fit="fill"></el-image>

      </el-col>
    
  </el-row>
    
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
      fit: 'fill',
      // 显示 本地图片
      //url: require('../../assets/img/lotus.jpeg'),
      url: 'https://gitee.com/ssdls/blogimg/raw/master/img/20210202190453.gif',
      url2: 'http://acg.67jy.top/template/nex_manga_181008/neoconex/index/ads2.jpg',
      HotSeeList:[{
        href: '/',
        title: '高洁璀璨的绿宝石 花京院典明（花京院个人'
      },
      {
        href: '/',
        title: '高洁璀璨的绿宝石 花京院典明（花京院个人'
      },
      {
        href: '/',
        title: '高洁璀璨的绿宝石 花京院典明（花京院个人'
      },
      {
        href: '/',
        title: '高洁璀璨的绿宝石 花京院典明（花京院个人'
      },
      {
        href: '/',
        title: '高洁璀璨的绿宝石 花京院典明（花京院个人'
      }

      ]
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //方法集合
  methods: {
    handlerClick(){
      console.log(1)
    }
  },
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
<style lang="scss" >
    @import "@/assets/css/index/hotsee.scss";
</style>