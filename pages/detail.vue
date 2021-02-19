<template>
  <div class="page-detail">
    <el-row>
      <el-col :span="24">
        <crumbs :keyword="keyword" :type="type" />
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <summa :meta="product" />
      </el-col>
    </el-row>
    <el-row class="m-title">
      <el-col :span="24">
        <h3
          style="font-size: 20px;line-height: 26px; margin-top:-25px; margin-bottom: 30px;"
        >商家团购及优惠</h3>
      </el-col>
    </el-row>
    <!-- 当能购买或者没有登录时显示模块 -->
    <el-row v-if="canOrder || !login">
      <el-col :span="19">
        <list v-if="login" :list="list" />
        <div v-else class="deal-need-login">
          <img src="//p0.meituan.net/codeman/56a7d5abcb5ce3d90fc91195e5b5856911194.png" alt="登录查看" />
          <span>请登录后查看详细团购优惠</span>
          <el-button @click="toLogin" type="primary" round>立即登录</el-button>
        </div>
        <comment></comment>
      </el-col>
      <el-col :span="5">
        <lovely></lovely>
      </el-col>
    </el-row>
    <el-backtop></el-backtop>
  </div>
</template>

<script>
import Crumbs from "@/components/detail/crumbs.vue";
import Summa from "@/components/detail/summary.vue";
import List from "@/components/detail/list.vue";
import Comment from "@/components/detail/comment.vue";
import Lovely from "@/components/products/lovely.vue";
export default {
  data() {
    return {
      keyword: "",
      product: {},
      type: "",
      list: [],
      login: false
    };
  },
  components: {
    Crumbs,
    Summa,
    List,
    Lovely,
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
@import "@/assets/css/detail/index.scss";
</style>
