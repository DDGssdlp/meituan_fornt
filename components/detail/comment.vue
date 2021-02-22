<template>
  <div class="comment">
    <div class="total">
      <div class="sort">
        <span class="on">质量排序</span>
        <span class>时间排序</span>
      </div>{{list.length}}条网友点评
    </div>
    <el-card class="comment-card" shadow="never">
      <div class="see">
        <el-checkbox v-model="checked">只看有图片的评论</el-checkbox>
      </div>
      <el-card class="comment-inner-card" shadow="never" v-for="(comment, idx) in list" :key="idx">
        <el-row>
          <el-col :span="2">
            <div class="grid-content bg-purple">
              <el-avatar :size="size" :src="comment.headSrc"></el-avatar>
            </div>
          </el-col>
          <el-col :span="22">
            <div class="grid-content bg-purple-light">
              <div class="info">
                <div class="name">{{comment.name}}</div>
                <span class="rate-img">
                  <el-rate v-model="comment.rate" disabled text-color="#ff9900" :colors="colors"></el-rate>
                </span>
                <div class="date">
                  <span>{{comment.date}}</span>
                </div>

                <div class="desc">{{comment.desc}}</div>
              </div>
              <div class="info-imgs">
                <el-row>
                  <el-col class="img-col" :span="5" v-for="(item, idx) in comment.imgList" :key="idx">
                    <div class="img">
                      <el-avatar shape="square" :size="size" :fit="fit" :src="item"></el-avatar>
                    </div>
                  </el-col>
                </el-row>
              </div>
              <div class="divider">
                <el-divider></el-divider>
              </div>
            </div>
          </el-col>
        </el-row>
      </el-card>
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
    </el-card>
  </div>
</template>

<script>
export default {
  props: {
    list: {
      type:Array
    }
  },
  methods: {
    currentChangeHandle(val) {
        this.pageIndex = val;
    }
  },
  data() {
    return {
      colors: ["#99A9BF", "#F7BA2A", "#FF9900"],
      size: "large",
      fit: "fill",
      pageIndex: 1,
      pageSize: 2,
      totalPage: 0,
      checked: false,
      rate: 4
    };
  }
};
</script>
<style lang='scss' >
@import "@/assets/css/detail/comment.scss";
</style>