<template>
  <div class="m-products-list">
    <dl>
      <dd
        v-for="item in nav"
        :key="item.name"
        :class="[item.name,item.acitve?'s-nav-active':'']"
        @click="navSelect"
      >{{ item.txt }}</dd>
    </dl>
    <ul>
      <Item v-for="(item,idx) in list" :key="idx" :meta="item" />
    </ul>
    <div class="pageSize">
      <el-pagination
        @current-change="currentChangeHandle"
        :current-page="pageIndex"
        :page-size="pageSize"
        :total="totalPage"
        background
        layout="prev, pager, next"
      ></el-pagination>
    </div>
  </div>
</template>

<script>
import Item from "./product.vue";
export default {
  components: {
    Item
  },
  props: {
    // list: {
    //   type: Array,
    //   default() {
    //     return [];
    //   }
    // }
  },
  data() {
    return {
      pageIndex: 1,
      pageSize: 5,
      totalPage: 0,
      list: [
        // {brandId:1,name: "张三丰小吃店",rate:3,img:"https://edu-ddg.oss-cn-beijing.aliyuncs.com/2021/02/05/cd2c95a8085e44c5b2c75522a5c0caad4.jpg",type:"景店",addr:"null",price: 100,status:"新店",comment:3699},
      ],
      nav: [
        {
          name: "s-default",
          txt: "智能排序",
          acitve: true
        },
        {
          name: "s-price",
          txt: "价格最低",
          active: false
        },
        {
          name: "s-visit",
          txt: "人气最高",
          active: false
        },
        {
          name: "s-comment",
          txt: "评价最高",
          active: false
        }
      ]
    };
  },
  async asyncData({ app }) {
    // let { data } = await app.$axios.get(`/product/brand/list/page`, {
    //       params: {
    //         cartId: catId,
    //         page: this.pageIndex,
    //         limit: this.pageSize,
    //       }
    //     })
    // console.log("data", data);
    // return { items: data.list };
  },
  created() {
    this.getList();
  },
  methods: {
    currentChangeHandle(val) {
      this.pageIndex = val;
      this.getList();
    },
    navSelect: function(el) {
      let navr = this.nav;
      let activeClass = el.target.className;
      this.nav.forEach(element => {
        if (element.name == activeClass) {
          element.active = true;
          el.target.className += " s-nav-active";
        }
      });
    },
    getList: function() {
      let catId = this.$route.query.search;
      //let cat = JSON.parse('[{"brandId":1,"name":"张三丰小吃店","rate":4,"img":"https://edu-ddg.oss-cn-beijing.aliyuncs.com/2021/02/05/cd2c95a8085e44c5b2c75522a5c0caad4.jpg","type":"景店","addr":null,"status":"新店","comment":6910},{"brandId":2,"name":"张三丰炸鸡店","rate":0,"img":"https://edu-ddg.oss-cn-beijing.aliyuncs.com/2021/02/05/7b97e7980484490080c58c68fa5920bb2.jpg","type":"景店","addr":null,"status":"新店","comment":7132},{"brandId":3,"name":"赵六","rate":4,"img":"https://edu-ddg.oss-cn-beijing.aliyuncs.com/2021/02/05/be449399a1e14715aee397e0546c87dd1.jpg","type":"景店","addr":null,"status":"新店","comment":849}]')
      // this.list =  cat;
      this.$axios
        .get(`/product/brand/list/page`, {
          params: {
            cartId: catId,
            page: this.pageIndex,
            limit: this.pageSize
          }
        })
        .then(data => {
         
          this.totalPage = data.data.page.totalCount;
          this.list = data.data.page.list;
        })
        .catch(err => {});
    }
  }
};
</script>

<style>

</style>>
