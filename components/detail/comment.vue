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
                  <el-col class="img-col" :span="5" v-for="(item, idx) in comment.imgList.slice(0, 3)" :key="idx">
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

      list: [
        {
          headSrc:
            "https://img.meituan.net/avatar/34d5bb59ef2d0b6a1e7e7af0a993a95f22548.jpg",
          name: "美团-张三丰",
          rate: 4,
          date: "2020年10月10日",
          desc:
            "越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧",
          imgList: [
            
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg"
          ]
        },
        {
          headSrc:
            "https://img.meituan.net/avatar/34d5bb59ef2d0b6a1e7e7af0a993a95f22548.jpg",
          name: "美团-张三丰",
          rate: 4,
          date: "2020年10月10日",
          desc:
            "越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧",
          imgList: [
            // "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg",
            // "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg",
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg"
          ]
        },
        {
          headSrc:
            "https://img.meituan.net/avatar/34d5bb59ef2d0b6a1e7e7af0a993a95f22548.jpg",
          name: "美团-张三丰",
          rate: 4,
          date: "2020年10月10日",
          desc:
            "越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧越来越贵了 快吃不起披萨了 披萨虽然很好吃 但真的是太贵太贵了 店铺活动少 没办法 如果不是带孩子来 应该不会再来了 主要是服务员的态度真的不太友好 好像我们吃不起披萨一样 要杯白开水都费死劲了 上菜慢的要死 大家慎重选择前往吧",
          imgList: [
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg",
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg",
            "https://p0.meituan.net/shaitu/baebe7c492940864ed334262097c78a9269667.jpg"
          ]
        }
      ],
      checked: false,
      rate: 4
    };
  }
};
</script>
<style lang='scss' >
@import "@/assets/css/detail/comment.scss";
</style>