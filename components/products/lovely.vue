<template>
  <div class="lovely">
    <el-card class="lovely-card" shadow="never">
      <h3>猜你喜欢</h3>
      <el-card
        class="inner-card"
        shadow="never"
        v-for="(item, idx) in lovelyList.slice(0, 5)"
        :key="idx"
      >
        <!-- 使用 nuxt link 会导致不能进行页面跳转 -->
        <a v-bind="{href:'/detail?brandId='+ item.brandId}">
          <img class="img" :src="url" alt="_blank" />
          <p class="name">{{item.brandName}}</p>
          <p class="desc">{{item.addr}}</p>
          <p class="price">
            <b>￥</b>
            {{item.price}}
          </p>
       </a>
      </el-card>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url:
        "https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg",
      fit: "fill",
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
          brandId: 8,
          brandName: "火炉火烤肉·芝士排骨（西红门荟聚购物中心店）",
          addr: "西红门",
          price: "210.0"
        }
      ]
    };
  },
  methods: {
    
  }
};
</script>
<style>
</style>>