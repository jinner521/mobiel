<template>
  <div>
    <div class="header">
      <h3>
        <i class="iconfont icon-demo1" @click="$router.go(-1)"></i> 小U商城
      </h3>
      <div class="search">
        <i class="iconfont icon-sousuo"></i>
        <input type="text" name="" id="" placeholder="按内容搜索" />
      </div>
      <div class="nav">
        <van-list  v-if="goodsList.length > 0">
          <van-card
          checked=false
            v-for="item in goodsList"
            :key="item.id"
            :price="item.price.toFixed(2)"
            desc="描述信息"
            :title="item.goodsname"
            :thumb="
              item.img
                ? $imgUrl + item.img
                : 'https://img.yzcdn.cn/vant/ipad.jpeg'"

            @click="goDetail(item.id)"
          />

        </van-list>
        <van-list v-else><van-empty description="暂无商品"/></van-list>
        
      </div>
    </div>
  </div>
</template>

<script>
import { getGoods } from "../util/axios";
export default {
  data() {
    return {
      goodsList: [],
    };
  },
  mounted() {
    getGoods({
      fid: this.$route.query.id,
    }).then((res) => {
      console.log(res, "商品列白哦");
      if (res.code == 200) {
        this.goodsList = res.list ? res.list : [];
      }
    });
  },
  methods: {
    // 封装一个跳转详情事件
    goDetail(id){
      this.$router.push({
        path:'/detail',
        query:{
          id
        }
      })
    }
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
.header h3 .icon-demo1 {
  font-size: 0.48rem;
  position: absolute;
  left: 0.32rem;
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
</style>
