<template>
  <el-row class="page-product">
    <el-col :span="19">
      <crumbs :keyword="keyword" />
      <categroy :types="types" :areas="areas" />
      <list :list="list" />
    </el-col>
    <el-col :span="5">
      <amap v-if="point.length" :width="230" :height="250" :point="point" />
      <lovely></lovely>
    </el-col>
  </el-row>
</template>

<script>
import Crumbs from "@/components/products/crumbs.vue";
import Categroy from "@/components/products/categroy.vue";
import List from "@/components/products/list.vue";
import Lovely from "@/components/products/lovely.vue";
import Amap from "@/components/public/map.vue";

export default {
  components: {
    Crumbs,
    Categroy,
    List,
    Lovely,
    Amap
  },
  data() {
    return {
      list: [],
      types: [],
      areas: [],
      geoLocaltion: "",
      keyword: "",
      point: []
    };
  },
  mounted() {
    this.getGeoLocation();
     
  },
  methods: {
    getGeoLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          function(position) {
            this.geoLocaltion  = `${position.coords.longitude}, ${position.coords.latitude}` 
            this.point = this.geoLocaltion.split(',')
            console.log(this.point)
          },
          function(error) {   
          }
        );
      }
      this.geoLocaltion = '116.368904,39.913423'
      this.point = this.geoLocaltion.split(',')
      console.log(this.point)
    }
    //  currentChangeHandle(val) {
    //   this.pageIndex = val;
    //   this.getList();
    // },
  
  },
  async asyncData(ctx) {
    
  }
};
</script>

<style lang="scss">
@import "@/assets/css/products/index.scss";
</style>
