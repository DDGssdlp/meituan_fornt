<template>
  <section class="m-istyle">
    <dl @mouseover="over">
      <dt>有格调</dt>
      <dd :class="{active:kind==='all'}" kind="all" keyword="景点">全部</dd>
      <dd :class="{active:kind==='part'}" kind="part" keyword="美食">约会聚餐</dd>
      <dd :class="{active:kind==='spa'}" kind="spa" keyword="丽人">丽人SPA</dd>
      <dd :class="{active:kind==='movie'}" kind="movie" keyword="电影">电影演出</dd>
      <dd :class="{active:kind==='travel'}" kind="travel" keyword="旅游">品质出游</dd>
    </dl>
    <ul class="ibody">
      <li v-for="(item, index) in curList" :key="index">
        <el-card :body-style="{ padding: '0px' }" shadow="hover">
          <img class="my-img" @click="handlerCilck" :src="item.img" :class="item.title" />
          <ul class="cbody">
            <li class="title">{{ item.title }}</li>
            <li class="pos">
              <span>{{ item.pos }}</span>
            </li>
            <li class="price">
              ￥
              <em>{{ item.price }}</em>
              <span>/起</span>
            </li>
          </ul>
        </el-card>
      </li>
    </ul>
  </section>
</template>
<script>
export default {
  data: () => {
    return {
      kind: "all",
      curList: [
        {
          title: "张三",
          pos: "保岱镇",
          price: 666,
          img:
            "https://img.meituan.net/phoenix/14bc46b5740b7714df2dc3fbf27b542d1459696.jpg@1920w_1080h"
        },
        {
          title: "张三",
          pos: "保岱镇",
          price: 666,
          img:
            "https://img.meituan.net/phoenix/14bc46b5740b7714df2dc3fbf27b542d1459696.jpg@1920w_1080h"
        },
        {
          title: "张三",
          pos: "保岱镇",
          price: 666,
          img:
            "https://img.meituan.net/phoenix/14bc46b5740b7714df2dc3fbf27b542d1459696.jpg@1920w_1080h"
        },
        {
          title: "张三",
          pos: "保岱镇",
          price: 666,
          img:
            "https://img.meituan.net/phoenix/14bc46b5740b7714df2dc3fbf27b542d1459696.jpg@1920w_1080h"
        },
        {
          title: "张三",
          pos: "保岱镇",
          price: 666,
          img:
            "https://img.meituan.net/phoenix/14bc46b5740b7714df2dc3fbf27b542d1459696.jpg@1920w_1080h"
        },
        {
          title: "张三",
          pos: "保岱镇",
          price: 666,
          img:
            "https://img.meituan.net/phoenix/14bc46b5740b7714df2dc3fbf27b542d1459696.jpg@1920w_1080h"
        }
      ],
      city: "北京",
      list: {
        all: [],
        part: [],
        spa: [],
        movie: [],
        travel: []
      }
    };
  },
  computed: {
    cur: function() {
      return this.list[this.kind];
    }
  },
  async mounted() {
    let self = this;
    //console.log(self.$store.state.geo.position.city);

    // let {status,data:{count,pois}}=await self.$axios.get('/search/resultsByKeywords',{
    //   params:{
    //     keyword:'景点',
    //     city:self.city
    //   }
    // })
    // if(status===200&&count>0){
    //   let r= pois.filter(item=>item.photos.length).map(item=>{
    //     return {
    //       title:item.name,
    //       pos:item.type.split(';')[0],
    //       price:item.biz_ext.cost||'暂无',
    //       img:item.photos[0].url,
    //       url:'//abc.com'
    //     }
    //   })
    //   self.list[self.kind]=r.slice(0,9)
    // }else{
    //   self.list[self.kind]=[]
    // }
  },
  methods: {
    handlerCilck: async function(el) {
      console.log(el.target.className);
      this.$router.push(`/detail?title=${el.target.className}`);
    },
    over: async function(e) {
      let dom = e.target
      let tag = dom.tagName.toLowerCase()
      let self = this
      if (tag === 'dd') {
        this.kind = dom.getAttribute('kind')
        let keyword = dom.getAttribute('keyword')
    
      }
    }
  }
};
</script>
<style lang="scss">
@import "@/assets/css/index/artistic.scss";
</style>
