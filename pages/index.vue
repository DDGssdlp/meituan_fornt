<template>
  <div class="page-index">
    <el-row>
      <el-col :span="5">
        <emenu/>
      </el-col>
      <el-col :span="19">
        <life/>
      </el-col>
       </el-row>
    <el-row :span="24">
        <hot-see/>
    </el-row>
   
    <el-row :span="24">
        <artistic/>
    </el-row>
     <el-row :span="24">
        <recommend/>
    </el-row>
     <el-row :span="24">
        <fashion/>
    </el-row>
    <el-row :span="24">
        <navigation/>
    </el-row>
     <el-backtop ></el-backtop>
  </div>
</template>

<script>
import Emenu from '@/components/index/menu.vue'
import Life from '@/components/index/life.vue'
import Artistic from '@/components/index/artistic.vue'
import Fashion from '@/components/index/fashion.vue'
import Recommend from '@/components/index/Recommend.vue'
import HotSee from '@/components/index/HotSee.vue'
import Navigation from '@/components/index/navigation.vue'

export default {
  components: {
    Emenu,
    Life,
    Artistic,
    Recommend,
    HotSee,
    Fashion,
    Navigation
  }
}
</script>
 
<style lang="scss">
  @import "@/assets/css/index/index.scss";
</style>