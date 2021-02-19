<template>
  <div class="m-detail-list">
    <ul>
      <!-- <li>{{list.filter(item=>item.photos.length).length}}款套餐</li> -->
      <li class="data-li">{{list.length}}款堂食套餐</li>
      <item v-for="(item,idx) in showList" :key="idx" :meta="item" />
      <el-link type="info" @click="handleClick" :underline="false">
        {{this.info && list.length - this.slice > 0 ?this.info: ""}}
        <i
          v-if="(this.info && list.length - this.slice > 0 )"
          :class="classname"
        ></i>
      </el-link>
    </ul>
  </div>
</template>

<script>
import Item from "./item";
export default {
  // props:{
  //     list:{
  //         type:Array,
  //         default:()=>{
  //             return
  //         }
  //     }
  // },
  components: {
    Item
  },
  data() {
    return {
      click: true,
      info: "",
      slice: 2,
      showList: [],
      classname: "el-icon-caret-bottom",
      list: [
        {
          photos: [
            {
              url:
                "https://p0.meituan.net/208.126/deal/1d8077d7f64aec1271e848415a12081a32283.jpg",
              title: "1"
            }
          ],
          name: "奶茶",
          deadline: "7天",
          biz_ext: {
            ticket_ordering: 100,
            cost: 90
          }
        },
        {
          photos: [
            {
              url:
                "https://p0.meituan.net/208.126/deal/1d8077d7f64aec1271e848415a12081a32283.jpg",
              title: "1"
            }
          ],
          name: "奶茶",
          deadline: "3天",
          biz_ext: {
            ticket_ordering: 10,
            cost: 100
          }
        },
        {
          photos: [
            {
              url:
                "https://p0.meituan.net/208.126/deal/1d8077d7f64aec1271e848415a12081a32283.jpg",
              title: "1"
            }
          ],
          name: "奶茶",
          deadline: "3天",
          biz_ext: {
            ticket_ordering: 10,
            cost: 100
          }
        }
      ]
    };
  },
  mounted() {
    this.showList = this.list.slice(0, this.slice);
    this.info = `更多${this.list.length - this.slice}款套餐`;
  },
  methods: {
    handleClick() {
      if (this.click) {
        this.info = "收起";
        this.classname = "el-icon-caret-top";
        this.click = false;
        this.showList = this.list;
      } else {
        this.info = `更多${this.list.length - this.slice}款套餐`;
        this.classname = "el-icon-caret-bottom";
        this.click = true;
        this.showList = this.list.slice(0, this.slice);
      }
    }
  }
};
</script>
<style lang='scss'>
.m-detail-list .el-link--info {
  margin-top: 10px;
  margin-bottom: 10px;
  width: 100%;
}
.m-detail-list .el-link--info .el-link--inner {
  text-align: center;
}
</style>