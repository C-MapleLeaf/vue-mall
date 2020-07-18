<!--  -->
<template>
  <div id="home">
    <NavBar class="home-nav">
      <div slot="center">购物街</div>
    </NavBar>
    <home-swiper :banners="banners" />
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import HomeSwiper from "./chilsComps/HomeSwiper";
import { getHomeMultidata } from "../../network/home.js";
export default {
  components: {
    NavBar,
    HomeSwiper
  },
  data() {
    return {
      banners: [],
      recommends: []
    };
  },
  created() {
    // 1.请求多个数据
    getHomeMultidata().then(res => {
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    });
  }
};
</script>
<style scoped>
.home-nav {
  background-color: #fb7299;
  color: #fff;
}
</style>