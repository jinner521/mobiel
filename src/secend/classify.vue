<template>
  <div>
    <div class="header">
      <h3>分类</h3>
      <div class="search">
        <i class="iconfont icon-sousuo"></i>
        <input type="text" name="" id="" placeholder="按内容搜索" />
      </div>
    </div>
    <div class="content">
      <!-- 侧边栏 -->
      <van-sidebar v-model="activeKey" @change="onChange">
        <van-sidebar-item
          v-for="item in cateList"
          :key="item.id"
          :title="item.catename"
        />
      </van-sidebar>
      <!-- 二级分类展示 -->
      <van-grid :border="false" :gutter="10" :column-num="3">
        <van-grid-item :to="'/list?id='+item.id" v-for="item in secondList" :key="item.id">
          <van-image :src="item.img ? $imgUrl+item.img:'http://i.shouchaobao.vip/d/file/202003/i5pjz34dpy1.jpg'" />
       <p class="catetitle">{{item.catename}}</p>
        </van-grid-item>
      </van-grid>
    </div>
  </div>
</template>

<script>
import { getClassifyList } from "../util/axios";
export default {
  data() {
    return {
      activeKey: 0,
      cateList: [],
      secondList: [],
    };
  },
  mounted() {
    this.getCateInfo();
  },
  methods: {
    // 封装一个获取分类列表接口
    getCateInfo() {
      getClassifyList().then((res) => {
        if (res.code == 200) {
          //一级分类
          this.cateList = res.list;
          //二级分类
          this.secondList = res.list[0].children;
        }
        console.log(res, "分类列表");
      });
    },
    //封装一个左侧侧边栏切换的监听事件
    onChange() {
      console.log(this.activeKey, "activeKey");
      //当切换左侧侧边栏，动态获取二级分类
      this.secondList = this.cateList[this.activeKey].children;
    },
  },
};
</script>

<style lang="" scoped>
.header {
  padding-top: 0.88rem;
  position: relative;
  background-image: linear-gradient(180deg, #ff6040 0%, #ff8a80 100%);
  box-shadow: 0 2px 6px 0 rgba(255, 149, 128, 0.5);
}
.header h3 {
  text-align: center;
  color: white;
  font-weight: normal;
  height: 0.88rem;
  font-size: 0.48rem;
  line-height: 0.44rem;
}
.search {
  position: relative;
}
.header input {
  width: 6.7rem;
  height: 0.64rem;
  border-radius: 0.03rem;
  border: 1px solid transparent;
  outline: none;
  margin-left: 0.2rem;
  padding-left: 0.4rem;
  margin-bottom: 0.2rem;
}
.header .icon-sousuo {
  margin-right: 2%;
  font-size: 0.36rem;
  line-height: 0.64rem;
  position: absolute;
  color: #666;
  left: 0.25rem;
  top: 0.05rem;
}
.content {
  display: flex;
}
.van-grid {
  flex: 1;
}
.catetitle {
  font-size: 13px;
  color: #333;
}
.catetitle{
  color: #333;
  margin-top: .2rem;
}
</style>
