<!--  -->
<template>
  <TabBar>
    <TabBarItem path='/home'
                activeColor='blue'>
      <img slot="item-icon"
           src="~assets/img/tabbar/shouye.svg"
           alt="">
      <img slot="item-icon-active"
           src="~assets/img/tabbar/shouye_hover.svg"
           alt="">
      <div slot="item-text">首页</div>
    </TabBarItem>
    <TabBarItem path='/category'
                activeColor='blue'>
      <img slot="item-icon"
           src="~assets/img/tabbar/fenlei.svg"
           alt="">
      <img slot="item-icon-active"
           src="~assets/img/tabbar/fenlei_hover.svg"
           alt="">
      <div slot="item-text">分类</div>
    </TabBarItem>
    <TabBarItem path='/cart'
                activeColor='blue'>
      <img slot="item-icon"
           src="~assets/img/tabbar/baoshuicang.svg"
           alt="">
      <img slot="item-icon-active"
           src="~assets/img/tabbar/baoshuicang_hover.svg"
           alt="">
      <div slot="item-text">购物车</div>
    </TabBarItem>
    <TabBarItem path='/profile'
                activeColor='blue'>
      <img slot="item-icon"
           src="~assets/img/tabbar/wo.svg"
           alt="">
      <img slot="item-icon-active"
           src="~assets/img/tabbar/wo_hover.svg"
           alt="">
      <div slot="item-text">我的</div>
    </TabBarItem>
  </TabBar>
</template>

<script>
import TabBar from "../../common/tabbar/TabBar";
import TabBarItem from "../../common/tabbar/TarBarItem";
export default {
  components: {
    TabBar,
    TabBarItem
  }
};
</script>
<style scoped>
</style>