<template>
  <div>
    <!-- 导航栏 -->
    <div class="header">
      <h3>
        <i class="iconfont icon-demo1" @click="$router.go(-1)"></i> 个人中心
      </h3>
    </div>
    <!-- 头像 -->
    <div v-if="userInfo" class="imgInfo">
      <van-image
        round
        width="2.4rem"
        height="2.4rem"
        src="https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=3727176811,1187421040&fm=11&gp=0.jpg"
      />
      <!-- 用户名 -->
      <p class="nickname">{{ userInfo.nickname }}</p>
      <van-button @click="logout" type="danger">离开</van-button>
    </div>
    <!-- 未登录让他去登录 -->
    <div class="imgInfo" v-else>
      <van-image
        round
        width="2.4rem"
        height="2.4rem"
        src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimages.669pic.com%2Felement_pic%2F8%2F0%2F87%2F90%2F430fc441585d2fdc1018b7e87d479073.jpg&refer=http%3A%2F%2Fimages.669pic.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1613787247&t=e67de3f011af23b94547cbbb96f1366f"
      />
      <!-- 用户名 -->
      <p class="nickname">XXXX</p>
      <van-button @click="$router.push('/login')" type="warning"
        >去登录</van-button
      >
    </div>
    <div>
      <p>
        <van-cell title="地址管理" icon="location-o" /><van-icon class="arrow" name="arrow" />
      </p>
      <van-cell title="我的钱包" icon="gold-coin-o" /><van-icon class="arrow" name="arrow" />
      <van-cell title="我的二维码" icon="qr" /><van-icon class="arrow" name="arrow" />
      <van-cell title="我的小伙伴" icon="friends-o" /><van-icon class="arrow" name="arrow" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userInfo: {},
    };
  },
  mounted() {
    //把登录信息从存储中取出来
    this.userInfo = sessionStorage.getItem("userInfo")
      ? JSON.parse(sessionStorage.getItem("userInfo"))
      : false;

    console.log(this.userInfo, "userInfouserInfouserInfo");
  },
  methods: {
    //封装一个退出登录事件
    logout() {
      //清空你的缓存并强制跳转到登录
      sessionStorage.removeItem("userInfo");
      this.$router.push("/login");
    },
  },
};
</script>

<style  lang="" scoped>
.header {
  padding-top: 0.88rem;
  height: 1.2rem;
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
.imgInfo {
  text-align: center;
}
.nickname {
  font-size: 24px;
  color: #333;
}
.van-button {
  margin-top: 0.2rem;
  height: 0.4rem;
}
.arrow {
  float: right;
  display: inline-block;
  margin-top: -.4rem;
  font-size: 16px;
  font-weight: lighter;
}
</style>
