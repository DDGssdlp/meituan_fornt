<template>
  <dl class="sum-card">
    <dd>
      <el-carousel height="304px" indiicator-position="none">
        <el-carousel-item v-for="(item,idx) in meta.photos" :key="idx">
          <el-image :src="item" :fit="fit"></el-image>
        </el-carousel-item>
      </el-carousel>
    </dd>
    <dt>
      <h1>{{meta.name}}</h1>
      <el-rate v-model="meta.rate" disabled />
      <!-- <span>{{Number(meta.biz_ext.rating)||rate}}分</span>
      <span>人均￥{{Number(meta.biz_ext.cost)}}</span>-->
      <span>{{meta.rate}}分</span>
      <span>人均￥{{ meta.price}}</span>

      <ul>
        <li>
          地址: {{meta.address}}
          <a>
            <i class="el-icon-location" @click="openMap(meta.locaton)"></i>
          </a>
        </li>
        <li>电话: {{meta.tel}}</li>
        <li>营业时间：{{meta.openDate}}</li>
         
      </ul>
      <div class="rount">
          <el-button type="warning" round @click="createCart">立即抢购</el-button>
      </div>
       
    </dt>
   
  </dl>
  
</template>

<script>
export default {
  props: {
    // meta:{
    //     type:Object,
    //     default:()=>{
    //         return {}
    //     }
    // }
  },
  created() {
    this.getMenu();
  },
  data() {
    return {
      fit: "fill",
      meta: {
        name: "张三李四王五",
        rate: 4,
        address: "",
        openDate: "周一至周日 11:00-21:00",
        tel: "010-678488",
        price: 200,
        photos: []
      },
      rate: 4,
      sale: 70 + Math.floor(Math.random() * 300)
    };
  },
  computed: {
    //rate:function(){
    // return Number(this.meta.biz_ext.rating) || Math.floor(Math.random()*5)
    //}
  },
  methods: {
    createCart() {
      this.$router.push("/cart");
    },
    openMap: function(location) {
      this.$message({
        message: "功能待开发！",
        type: "success"
      });
    },
    getMenu: async function() {
      let brandId = this.$route.query.brandId;
      await this.$axios
        .get(`/product/brand/info/${brandId}`)
        .then(res => {
          if (res.data && res.data.code === 0) {
            let brand = res.data.brand;
            this.meta.name = brand.name;
            this.meta.photos = brand.images
              .split(",")
              .slice(0, brand.images.split(",").length - 1);
            this.meta.address = brand.address;
          }
        })
        .catch(err => {});
    }
  }
};
</script>
<style lang='scss'>

</style>