<template>
  <div class="m-product-categroy">
    <dl class="classic">
      <dt>分类</dt>
      <dt>全部</dt>
      <dd v-for="(item,idx) in numbers.slice(0, 6)" :key="idx">
        <div class="m-product-select">
          <dl class="tab">
            <dt>{{ item.type }}</dt>
          </dl>
        </div>
      </dd>
    </dl>
    <dl class="classic" style="margin-left: 160px;">
      <dd v-for="(item,idx) in numbers.slice(6, 12)" :key="idx">
        <div class="m-product-select">
          <dl class="tab">
            <dt>{{ item.type }}</dt>
          </dl>
        </div>
      </dd>
    </dl>
    <dl class="classic" style="margin-left: 160px;margin-bottom: -20px;">
      <dd v-for="(item,idx) in numbers.slice(6, 12)" :key="idx">
        <div class="m-product-select">
          <dl class="tab">
            <dt>{{ item.type }}</dt>
          </dl>
        </div>
      </dd>
    </dl>
    <el-divider></el-divider>
    <dl class="classic">
      <dt>区域</dt>
      <dt>全部</dt>
      <dd v-for="(item,idx) in numbers.slice(0,6)" :key="idx">
        <iselect :name="item.type" :list="item.module" />
      </dd>
    </dl>
    <dl class="classic" style="margin-left: 160px;">
      <dd v-for="(item,idx) in numbers.slice(6,12)" :key="idx">
        <iselect :name="item.type" :list="item.module" />
      </dd>
    </dl>
    <dl class="classic" style="margin-left: 160px; margin-bottom: -20px;">
      <dd v-for="(item,idx) in numbers.slice(13,18)" :key="idx">
        <iselect :name="item.type" :list="item.module" />
      </dd>
    </dl>
    <el-divider></el-divider>
    <dl class="classic">
      <dt>用餐人数</dt>
      <dt>全部</dt>
      <dd v-for="(item,idx) in numbers.slice(0, 6)" :key="idx">
        <div class="m-product-select">
          <dl class="tab">
            <dt>{{ item.type }}</dt>
          </dl>
        </div>
      </dd>
    </dl>
    <dl class="classic" style="margin-left: 160px;">
      <dd v-for="(item,idx) in numbers.slice(6, 12)" :key="idx">
        <div class="m-product-select">
          <dl class="tab">
            <dt>{{ item.type }}</dt>
          </dl>
        </div>
      </dd>
    </dl>
  </div>
</template>

<script>
import iselect from "./iselect.vue";
export default {
  components: {
    iselect
  },
  data() {
    return {
      numbers: [
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" },
        { type: "单人餐", List: "" }
      ]
    };
  },
  mounted() {
    console.log(this.numbers);
    this.getLength();
  },
  methods: {
    
    getLength() {
      this.numbers = this.numbers.slice(0, 18);
    }
  },
  props: {
    types: {
      type: Array,
      default() {
        return [];
      }
    },
    areas: {
      type: Array,
      default() {
        return [];
      }
    }
  }
};
</script>

<style lang="scss">
</style>
