<template>
  <div class="m-order">
    <ul>
      <li v-if="cur.length">
        <el-row v-for="(item, idx) in cur" :key="idx">
          <el-col :span="4">
            <img :src="item.img" alt="">
          </el-col>
          <el-col :span="10">
            <h4>{{ item.name }}</h4>
            <p>数量: {{ item.count }}</p>
          </el-col>
          <el-col :span="4">
            总价: ￥ {{ item.total }}
          </el-col>
          <el-col :span="6">
            {{ item.statusTxt }}
          </el-col>
        </el-row>
      </li>
      <li
        v-else
        class="empty">
        <div class="order-img">
          <el-image
          class="imgnoorder"
          :src="url"
          :fit="fit"></el-image>

          <div class="order-font">这里目前还是空空如也</div> 
        </div>
        <div>
         
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data(){
   return {
     url: "https://gitee.com/ssdls/blogimg/raw/master/img/20210202182647.png",
     fit: "fill"
   }
  },
  props: {
    cur: {
      type: Array,
      default: () => {
        return []
      }
    }
  }
}
</script>

<style lang="scss">


</style>