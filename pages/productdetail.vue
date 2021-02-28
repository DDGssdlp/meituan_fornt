<template>
  <div class>
    <el-row>
      <el-col :span="24">
        <el-card class="box-card">
          <summa />
        </el-card>
      </el-col>
    </el-row>
    <el-row>
      <affix :offset="50">
        <el-card>
          <el-col :span="23">
            <el-tabs class="tabs" v-model="activeName" @tab-click="goAnchor">
              <el-tab-pane label="适用门店" name="mendian"></el-tab-pane>
              <el-tab-pane label="团购详情" name="tuangou"></el-tab-pane>
              <el-tab-pane label="购买须知" name="goumai"></el-tab-pane>
              <el-tab-pane label="用户评价" name="pinglun"></el-tab-pane>
            </el-tabs>
          </el-col>
        </el-card>
      </affix>
    </el-row>

    <el-row>
      <el-col :span="24">
        <div id="anchor-mendian" class="item"></div>
        <h3 class="detail-title">适用门店</h3>
        <el-card class="mendian" shadow="never"></el-card>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <div id="anchor-tuangou" class="item"></div>
        <h3 class="detail-title">团购详情</h3>
        <el-card class="tuangou" shadow="never"></el-card>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <div id="anchor-goumai" class="item"></div>
        <h3 class="detail-title">购买须知</h3>
        <el-card class="goumai" shadow="never"></el-card>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <h3 class="detail-title">商品详情</h3>
        <el-card class="xiangqing" shadow="never"></el-card>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <div id="anchor-pinglun" class="item"></div>
        <h3 class="detail-title">用户评价</h3>
        <comment :list="list"></comment>
      </el-col>
    </el-row>
    <el-backtop></el-backtop>
  </div>
</template>

<script>
import Affix from "easy-affix";
import Summa from "@/components/productdetail/productSummary.vue";
import Comment from "@/components/detail/comment.vue";
export default {
  data() {
    return {
      activeName: "",
      keyword: "",
      product: {},
      type: "",
     list: [
        {
          headSrc:
            "https://img.meituan.net/avatar/34d5bb59ef2d0b6a1e7e7af0a993a95f22548.jpg",
          name: "美团-张三丰",
          rate: 4,
          date: "2020年10月10日",
          desc:
            "越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧",
          
        },
        {
          headSrc:
            "https://img.meituan.net/avatar/34d5bb59ef2d0b6a1e7e7af0a993a95f22548.jpg",
          name: "美团-张三丰",
          rate: 4,
          date: "2020年10月10日",
          desc:
            "越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧",
          imgList: [
            // "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg",
            // "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg",
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg"
          ]
        },
        {
          headSrc:
            "https://img.meituan.net/avatar/34d5bb59ef2d0b6a1e7e7af0a993a95f22548.jpg",
          name: "美团-张三丰",
          rate: 4,
          date: "2020年10月10日",
          desc:
            "越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧",
          imgList: [
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg",
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg",
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg"
          ]
        }
      ],
      login: false
    };
  },
  components: {
    Affix,
    Summa,
    Comment
  },
  mounted() {
    this.checkLogin();
  },
  computed: {
    //通过是否有图片判断当前产品能否购买，模拟上线购买状态
    canOrder: function() {
      return true;
      // return this.list.filter(item=>item.photos.length).length
    }
  },
  methods: {
    // 实现锚点
    goAnchor() {
      let selector = `#anchor-${this.activeName}`;
      document.querySelector(selector).scrollIntoView(true);
    },
    toLogin() {
      this.$router.push("/login");
    },
    checkLogin() {
      let loginUser = localStorage.getItem("loginUser");
      if (loginUser) {
        this.login = true;
        console.log(this.login);
      } else {
        this.login = false;
      }
    }
  },
  //asyncData返回的数据会merge原来data中的数据，所以data可以省去
  async asyncData(ctx) {
    //只有在服务端才能拿到keyword和type
    let { keyword, type } = ctx.query;
    // let {status,data:{product,more:list,login}}=await ctx.$axios.get('/search/products',{
    //   params:{
    //     keyword,
    //     type,
    //     city:ctx.store.state.geo.position.city
    //   }
    // })
    // if(status===200){
    //   return {
    //     keyword,
    //     product,
    //     type,
    //     list,
    //     login
    //   }
    // }else{
    //   return {
    //     keyword,
    //     product:{},
    //     type,
    //     list:[],
    //     login:false
    //   }
    // }
  }
};
</script>

<style lang="scss" >
@import "@/assets/css/productdetail/index.scss";
</style>
