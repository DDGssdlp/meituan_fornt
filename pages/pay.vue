<template>
  <div class="page-pay">
    <el-card class="box-card">
      <h3 style="text-align: center;">
        <i class="el-icon-time"></i>
        请在 {{datetime}} 内完成支付, 超时订单会自动取消
      </h3>
    </el-card>
    <el-card class="box-card">
      <el-row>
        <el-col :span="12">
          <div class="font-pay">
            <h2>项目：火炉火烤肉·芝士排骨2人餐</h2>
          </div>
        </el-col>
        <el-col :span="12">
          <div class="font-pay">
            <div class="amount">
              应付金额 ¥
              <span class="amount-price">218.00</span>
            </div>
          </div>
        </el-col>
      </el-row>
    </el-card>
    <el-card class="box-card">
      <el-tabs type="border-card" v-model="activeName" @tab-click="handleClick">
        <el-tab-pane label="支付宝/微信" name="first">
          <div class="card-size">
            <el-radio v-model="radio" @change="handleChange" label="微信">
              <img src="https://p1.meituan.net/pay/pc_wxqrpay.png" alt />
            </el-radio>
            <el-radio v-model="radio" @change="handleChange" label="支付宝">
              <img src="https://p0.meituan.net/pay/alipaypcnew.png" alt />
            </el-radio>
          </div>
          <div class="pay-buttom">
            <div class="font-pay">
              <div class="amount">
                支付 ¥
                <span class="amount-price">218.00</span>
              </div>
              <div class="pay-rount">
                <el-link href="/order" type="info" :underline="false" target="_blank">修改订单</el-link>
                <el-button class="button-pay" type="goon" :size="size" round @click="toPay">去付款</el-button>
              </div>
            </div>
          </div>
        </el-tab-pane>
        <el-tab-pane label="个人网银支付" name="second">
          <div class="card-size"></div>
        </el-tab-pane>
      </el-tabs>
    </el-card>

    <el-dialog :visible.sync="dialogVisible" width="800px" :before-close="handleClose">
      <el-row v-if="isWeChat">
        <el-col :span="12">
          <p>
            <span>请使用</span>
            <span class="orange">
              微信
              <i class="el-icon-full-screen"></i>
            </span>
            <i class="icon icon-qrcode"></i>
            <span class="orange">扫一扫</span>
            <br />扫描二维码支付
          </p>
          <div class="modal-qr">
            <div class="qrccode">
              <img class="modal-qrcode" :src="modleSRc" />
            </div>
            <p class="time">二维码有效时长为2小时, 请尽快支付</p>
          </div>
        </el-col>
        <el-col :span="12">
          <img
            class="pay-img"
            src="https://mpay.meituan.com/resource/cashier/img/weixin-qrcode.1xf1oN.jpg"
            alt
          />
        </el-col>
      </el-row>
      <el-row v-else>
        <el-col :span="12">
          <p>
            <span>请使用</span>
            <span class="orange">
              支付宝
              <i class="el-icon-full-screen"></i>
            </span>
            <i class="icon icon-qrcode"></i>
            <span class="orange">扫一扫</span>
            <br />扫描二维码支付
          </p>
          <div class="modal-qr">
            <div class="qrccode">
              <img class="modal-qrcode" :src="modleSRc" />
            </div>
            <p class="time">二维码有效时长为2小时, 请尽快支付</p>
          </div>
        </el-col>
        <el-col :span="12">
          <img
            class="pay-img"
            src="https://gitee.com/ssdls/blogimg/raw/master/img/20210203160317.jpg"
            alt
          />
        </el-col>
      </el-row>
    </el-dialog>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      modleSRc:
        "https://gitee.com/ssdls/blogimg/raw/master/img/20210203152359.png",
      dialogVisible: false,
      size: "large",
      activeLabel: "",
      radio: "1",
      activeName: "first",
      isWeChat: true,
      cart: [
        {
          name: "张三",
          price: 100,
          count: 1
        }
      ],
      datetime: "00:00:00",
      leftTime: 86400000,
      totalTime: 86400,
      flag: 0
    };
  },
  created() {
    this.start();
  },
  mounted() {},
  //计算total
  computed: {
    total() {
      let total = 0;
      this.cart.forEach(item => {
        total += item.price * item.count;
      });
      return total;
    }
  },
  methods: {
  
    handleChange(label) {
      this.activeLabel = label;
    },
    toPay() {
      if (this.activeLabel) {
        if (this.activeLabel === "微信") {
          this.isWeChat = true;
        } else {
          this.isWeChat = false;
        }
        this.dialogVisible = true;
      } else {
        this.$message({
          message: "请先选择支付方式！",
          type: "error"
        });
      }
    },
    handleClose() {
      this.dialogVisible = false;
    },
    handleClick() {},
    submit: async function() {
      location.href = "/order";
    },
    start() {
      this.leftTime = this.totalTime * 1000;
      this.countTime();
      this.flag += 1;
    },
    countTime() {
      
      this.leftTime = this.leftTime - 1000;

      //定义变量 d,h,m,s保存倒计时的时间
      if (this.leftTime >= 0) {
        this.h = Math.floor((this.leftTime / 1000 / 60 / 60) % 24);
        this.m = Math.floor((this.leftTime / 1000 / 60) % 60);
        this.s = Math.floor((this.leftTime / 1000) % 60);
      }

      //递归每秒调用countTime方法，显示动态时间效果
      this.datetime = this.h + ":" + this.m + ":" + this.s;
      if (this.flag < 2) {
        setTimeout(this.countTime, 1000);
      }
    }
  },
  //用ssr获取数据好处:1、体验好 2、保护接口，在服务端执行
  async asyncData(ctx) {}
};
</script>

<style lang="scss" scoped>
@import "@/assets/css/pay/index.scss";
</style>
