<!--  -->
<template>
  <div id="home">
    <NavBar class="home-nav">
      <div slot="center">购物街</div>
    </NavBar>
    <Scroll class="content"
            ref="scroll"
            :probe-type="3"
            @scroll="contentScroll"
            :pull-up-load="true"
            @pullingUp="loadMore">
      <home-swiper :banners="banners" />
      <recommend-view :recommends="recommends" />
      <Feature />
      <TabControl class="tab-control"
                  :titles="['流行','新款','精选']"
                  @tabClick="tabClick" />
      <GoodsList :goods="showGoods" />
    </Scroll>
    <BackTop @click.native="backClick"
             v-show="isShoeBackTop" />

  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import TabControl from "components/content/tabControl/TabControl";
import GoodsList from "components/content/goods/GoodsList";
import Scroll from "components/common/scroll/Scroll";
import BackTop from "components/content/backTop/BackTop";

import HomeSwiper from "./chilsComps/HomeSwiper";
import RecommendView from "./chilsComps/HomeRecommendView";
import Feature from "./chilsComps/FeatureView";

import { getHomeMultidata, getHomeGoods } from "../../network/home.js";

export default {
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    Feature,
    TabControl,
    GoodsList,
    Scroll,
    BackTop
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      },
      currentType: "pop",
      isShoeBackTop: false
    };
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    }
  },
  created() {
    // 1.请求多个数据
    this.getHomeMultidata();
    // 2.请求商品数据
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
  },
  methods: {
    // 事件监听
    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = "pop";
          break;
        case 1:
          this.currentType = "new";
          break;
        case 2:
          this.currentType = "sell";
          break;
        default:
          break;
      }
    },
    backClick() {
      this.$refs.scroll.scrollTo(0, 0, 500);
    },
    contentScroll(position) {
      this.isShoeBackTop = -position.y > 1000;
    },
    loadMore() {
      this.getHomeGoods(this.currentType);
    },
    // 网络请求
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        // console.log(res.data.list);
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
        this.$refs.scroll.finishPullUp();
      });
    }
  }
};
</script>
<style scoped>
#home {
  position: relative;
  padding-top: 44px;
  height: 100vh;
}
.home-nav {
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  width: 100%;
  background-color: #fb7299;
  color: #fff;
  z-index: 9;
}
.tab-control {
  position: sticky;
  top: 44px;
  z-index: 9;
  background-color: #fff;
}

/* 第一种方法 */
.content {
  height: calc(100% - 93px);
  overflow: hidden;
  margin-top: 44px;
}
/* 第二种方法 */
.content {
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  top: 0;
}
</style>