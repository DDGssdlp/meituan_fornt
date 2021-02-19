<template>
  <div class="m-menu">
    <dl class="nav" @mouseleave="mouseleave">
      <dt>全部分类</dt>
      <dd @mouseenter="mouseenter" v-for="(item,idx) in menu" :key="idx">
        <i :class="item.icon" />
        {{ item.name}}
        <span class="arrow" />>
      </dd>
    </dl>
    <div class="detail" v-if="kind" @mouseenter="sover" @mouseleave="sout">
      <template v-for="(item,idx) in curdetail.children.slice(0, 3)">
        <h4 :key="idx">{{ item.name }}</h4>
        <span
          v-for="v in item.children"
          :key="v.catId"
          :class="v.catId+ ''"
          @click="toOrder"
        >{{ v.name }}</span>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //记录鼠标hover时的类型
      kind: "",
      menu: []
    };
  },
  created() {
    this.getMenuList();
  },
  computed: {
    curdetail: function() {
      return this.menu.filter(item => item.icon === this.kind)[0];
    }
  },
  methods: {
    toOrder(el) {
      let login = localStorage.getItem("loginUser");
      if (login) {
        let ckeckedName = el.target.className;
        console.log(el.target)
        window.location.href = `/products?search=${ckeckedName}`;
      } else {
        this.$router.push("/login");
      }
    },
    getMenuList: async function() {
      await this.$axios
        .get(`/product/category/listWithTree`)
        .then(res => {
          this.menu = res.data.data;
        })
        .catch(err => {});
    },
    mouseleave: function() {
      let self = this;
      self._timer = setTimeout(function() {
        self.kind = "";
      }, 150);
    },
    mouseenter: function(e) {
      this.kind = e.target.querySelector("i").className;
    },
    sover: function() {
      clearTimeout(this._timer);
    },
    sout: function() {
      this.kind = "";
    }
  }
};
</script>
<style lang='scss' >
</style>