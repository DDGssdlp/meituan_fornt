<template>
  <div class="page-order">
    <el-row>
      <!-- 布局：分为左右两列 -->
      <el-col :span="4" class="navbar">
        <p class="meituan-my">
          <el-link href="/login" 
          :underline="false" 
          target="_blank" 
          class="title">我的美团</el-link>
        </p>
        <dl>
          <dt>我的订单</dt>
          <dd>
            全部订单
            <i class="el-icon-arrow-right" />
          </dd>
          <dd>
            待付款
            <i class="el-icon-arrow-right" />
          </dd>
          <dd>
            待使用
            <i class="el-icon-arrow-right" />
          </dd>
        </dl>
        <dl>
          <dt>我的收藏</dt>
          <dd>
            收藏的商家
            <i class="el-icon-arrow-right" />
          </dd>
          <dd>
            收藏的团购
            <i class="el-icon-arrow-right" />
          </dd>
        </dl>
        <dl>
          <dt>抵用卷</dt>
          <dd>
            可用卷
            <i class="el-icon-arrow-right" />
          </dd>
          <dd>
            失效卷
            <i class="el-icon-arrow-right" />
          </dd>
        </dl>
         <dl>
          <dt>
             <el-link href="/settings" :underline="false" target="_blank">个人信息</el-link>
           </dt>
          <dd>
            账户设置
            <i class="el-icon-arrow-right" />
          </dd>
        </dl>
        <el-divider></el-divider>
        <div class="m-life-downapp">
          <img src="//s1.meituan.net/bs/fe-web-meituan/60ac9a0/img/download-qr.png" alt="下载APP" />
          <p>美团APP手机版</p>
          <h4>
            <span class="red">1元起</span>
            <em class="gary">吃喝玩乐</em>
          </h4>
        </div>
      </el-col>
       
      <el-col :span="19" class="table">
        <el-tabs v-model="activeName" @tab-click="handleClick">
          <!-- name用做区分类型 -->
          <el-tab-pane label="全部订单" name="all">
            <!-- list就是订单信息 -->
            <list :cur="cur" />
          </el-tab-pane>
          <el-tab-pane label="待付款" name="unpay">
            <list :cur="cur" />
          </el-tab-pane>
          <el-tab-pane label="待使用" name="unuse">
            <list :cur="cur" />
          </el-tab-pane>
          <el-tab-pane label="待评价" name="unreplay">
            <list :cur="cur" />
          </el-tab-pane>
        </el-tabs>
      </el-col>
    </el-row>
    <el-row>
        <el-col>
          <navigation class="navigation-order"/>
        </el-col>
    </el-row>
    
    
   
  </div>
</template>

<script>
import List from "@/components/order/list.vue";
import Navigation from "@/components/index/navigation.vue";
export default {
  components: {
    List,
    Navigation
  },
  data() {
    return {
      activeName: "all",
      list: [],
      cur: []
    };
  },
  watch: {
    // 两个参数，newValue和oldValue
    activeName(val) {
      this.cur = this.list.filter(item => {
        if (val === "unpay") {
          return item.status === 0;
        } else if (val === "all") {
          return true;
        } else {
          return false;
        }
      });
    },
    list() {
      const val = this.name;
      this.cur = this.list.filter(item => {
        if (val === "unplay") {
          return item.status === 0;
        } else if (val === "all") {
          return true;
        } else {
          return false;
        }
      });
    }
  },
  methods: {
    handleClick(tab) {
      this.activeName = tab.name;
    }
  },
  async asyncData(ctx) {
    // const { status, data: { code, list }} = await ctx.$axios.post('/order/getOrders')
    // if (status === 200 && code === 0 && list.length) {
    //   return {
    //     // 将后端返回数据和前端数据进行映射
    //     list: list.map(item => {
    //       return {
    //         img: item.imgs.length ? item.imgs[0].url : 'https://i.loli.net/2019/01/10/5c3767c4a52de.png',
    //         name: item.name,
    //         count: 1,
    //         total: item.total,
    //         status: item.status,
    //         statusText: item.status === 0 ? '待付款' : '已付款'
    //       }
    //     }),
    //     cur: list.map(item => {
    //       return {
    //         img: item.imgs.length ? item.imgs[0].url : 'https://i.loli.net/2019/01/10/5c3767c4a52de.png',
    //         name: item.name,
    //         count: 1,
    //         total: item.total,
    //         status: item.status,
    //         statusText: item.status === 0 ? '待付款' : '已付款'
    //       }
    //     })
    //   }
    // }
  }
};
</script>

<style lang="scss">
@import "@/assets/css/order/index.scss";

</style>