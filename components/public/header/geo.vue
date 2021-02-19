<template>
  <div class="m-geo">
    <!-- store是vuex实例，state获取状态的，geo模块名称，position模块下的变量 -->
    <i class="el-icon-location"/>{{ city }}
    <nuxt-link
      class="changeCity"
      to="/changeCity">切换城市</nuxt-link>
    <!--[香河 廊坊 天津]-->
    <!--热门：{{hotPlaceList}}-->
    <!--{{$store.state.home.hotPlace.slice(0,3)}}-->
  </div>
</template>

<script>
export default {
  data(){
    return{
      hotPlaceList:[],
      city: '北京'
    }
  },
  async mounted() {
    // let self=this;
    // let {status,data:{result}}=await self.$axios.get('/search/hotPlace',{
    //   params:{
    //     city:this.city
    //   }
    // })
    // if(status===200&&result){
    //   self.hotPlaceList=result.slice(0,3);
    //   //console.log(self.hotPlaceList)
    //   if(self.hotPlaceList.length===0) self.hotPlaceList.name="该地区暂未发现";
    // }else{
    //   //console.log(`请求失败`+self.hotPlaceList)
    //   self.hotPlaceList.name="该地区暂未发现";
    // }
  },
}
</script>

<style lang="css">
</style>
