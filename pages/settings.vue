<template>
  <div class="page-order">
    <el-row>
      <!-- 布局：分为左右两列 -->
      <el-col :span="4" class="navbar">
        <p class="meituan-my">
          <el-link href="/login" :underline="false" target="_blank" class="title">我的美团</el-link>
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
          <dt>个人信息</dt>
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
        <h2>个人信息：</h2>
        <el-divider></el-divider>
        <el-row class="settings-info">
          <el-col :span="2">
            <h3>头像</h3>
          </el-col>
          <el-col :span="1">
            <el-divider direction="vertical"></el-divider>
          </el-col>
          <el-col :span="17">
            <div class="settins-font">
              <el-avatar :size="size" :fit="fit" :src="defaultUrl"></el-avatar>
            </div>
          </el-col>
          <el-col :span="4">
            <el-button round>修改</el-button>
          </el-col>
        </el-row>
        <el-row class="settings-info">
          <el-col :span="2">
            <h3>昵称</h3>
          </el-col>
          <el-col :span="1">
            <el-divider direction="vertical"></el-divider>
          </el-col>
          
          <el-col :span="17">
            <div class="settins-font">{{user.userName}}</div>
          </el-col>
          <el-col :span="4">
            <el-button round>修改</el-button>
          </el-col>
        </el-row>
        <el-row class="settings-info">
          <el-col :span="2">
            <h3>生日</h3>
          </el-col>
          <el-col :span="1">
            <el-divider direction="vertical"></el-divider>
          </el-col>
          <el-col :span="17">
            <div class="settins-font">{{user.bitrhday}}</div>
          </el-col>
          <el-col :span="4">
            <el-button round>修改</el-button>
          </el-col>
        </el-row>
        <el-row class="settings-info">
          <el-col :span="2">
            <h3>绑定手机</h3>
          </el-col>
          <el-col :span="1">
            <el-divider direction="vertical"></el-divider>
          </el-col>
          <el-col :span="17">
            <div class="settins-font">{{user.phone}}</div>
          </el-col>
          <el-col :span="4">
            <el-button round>修改</el-button>
          </el-col>
        </el-row>
        <el-row class="settings-info">
          <el-col :span="2">
            <h3>登录密码</h3>
          </el-col>
          <el-col :span="1">
            <el-divider direction="vertical"></el-divider>
          </el-col>
          <el-col :span="17">
            <div class="settins-font">{{user.password}}</div>
          </el-col>
          <el-col :span="4">
            <el-button round>修改</el-button>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
    <el-row>
      <el-col>
        <navigation class="navigation-order" />
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
      size: "large",
      fit: "cover",
      defaultUrl:
        "",
      activeName: "all",
      list: [],
      cur: [],
      user: {
        userName: "张三",
        img: "1",
        bitrhday: "19960908",
        phone: "15613353227",
        password: "弱"
      }
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
  async mounted() {
    let loginUserPhone = localStorage.getItem("loginUser");
    if (loginUserPhone) {
      await this.$axios
        .get(`member/member/getLoginUser/${loginUserPhone}`)
        .then(res => {
          if (res.data.loginUser) {
            this.user.userName = res.data.loginUser.userName;
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
@import "@/assets/css/order/settings.scss";
</style>