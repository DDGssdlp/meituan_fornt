<template>
  <section class="m-istyle">
    <dl @mouseover="over">
      <dt>猜你喜欢</dt>
      <dd :class="{active:kind==='all'}" kind="all" keyword="最合适">为你甄选最适合的</dd>
    </dl>
    <ul class="ibody">
      <li v-for="(item, idx) in lovelyList.slice(0,10)" :key="idx">
        <el-card class="inner-card-fashion" shadow="never">
          <nuxt-link :to="{path:'/detail',query:{brandId:item.brandId}}">
            <img class="fashion-img" :src="url" alt="_blank" />
            <p class="name">{{item.brandName}}</p>
            <p class="desc">{{item.addr}}</p>
            <p class="price">
              <b>￥</b>
              {{item.price}}
            </p>
          </nuxt-link>
        </el-card>
      </li>
    </ul>
  </section>
</template>
<script>
export default {
  data: () => {
    return {
      url:
        "https://p1.meituan.net/mogu/cb6e5ed585e058d2862811174636e092223079.jpg",
      fit: "fill",
      kind: "all",
      lovelyList: [
        {
          brandId: 1,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 2,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 3,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 4,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        },
        {
          brandId: 5,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
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
  },
  methods: {
    over: async function(e) {}
  }
};
</script>
<style lang="scss" scoped>
@import "@/assets/css/index/fashion.scss";
</style>
