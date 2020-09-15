<template>
  <div id="home">
    <nav-bar class="home-nav">
      <template #center>购物街</template>
    </nav-bar>
    <tab-control
      :titles="['流行', '新款', '精选']"
      @tabClick="tabClick"
      ref="tabControl1"
      class="tabControl"
      v-show="isTabFixed"
    ></tab-control>
    <scroll
      class="homecontent"
      ref="scroll"
      :probe-type="3"
      :pull-up-load="true"
      @myscroll="contentScroll"
      @mypullingup="loadMore">
      <home-swiper :banners="banners"></home-swiper>
      <!-- <awesome :banners="banners"></awesome> -->
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view />
      <tab-control
        :titles="['流行', '新款', '精选']"
        @tabClick="tabClick"
        ref="tabControl2"
      ></tab-control>
      <goods-list :goods="showGoods"></goods-list>
    </scroll>
    <back-top @click="backTopClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import TabControl from "components/content/TabControl/TabControl";
import GoodsList from "components/content/goods/GoodsList";
import Scroll from "components/common/scroll/Scroll";
import BackTop from "components/content/backTop/BackTop";

import HomeSwiper from './childComps/HomeSwiper'
// import Awesome from './childComps/Awesome'

import RecommendView from "./childComps/ReCommendView";
import FeatureView from "./childComps/FeatureView";

import { getHomeMultidata, getHomeGoods } from "network/home";

export default {
  name: "Home",
  components: {
    NavBar,
    TabControl,
    GoodsList,
    Scroll,
    BackTop,
    HomeSwiper,
    RecommendView,
    FeatureView
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 1, list: [] },
        new: { page: 1, list: [] },
        sell: { page: 1, list: [] }
      },
      currentType: "pop",
      isShowBackTop: false,
      tabOffsetTop: 0,
      isTabFixed: false,
      temp: null
    };
  },
  created() {
    //请求多个数据
    this.getHomeMultidata();
    //请求商品数据
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");

    // 监听item中图片加载完成
    // this.$bus.$on('itemImageLoad', () => {
    //   this.$refs.scroll.refresh()
    // })
  },
  mounted() {
    this.temp = this.$refs.tabControl2.$el.offsetTop;
  },
  updated() {
    this.tabOffsetTop = this.temp;
  },
  methods: {
    /**
     * 事件监听相关
     */

    // 防抖函数
    // debounce(func, delay) {
    //   let timer = null
    //   return function(...arge) {
    //     if(timer) clearTimeout(timer)
    //     timer = setTimeout(() => {
    //       func.apply(this,args)
    //     }, delay);
    //   }
    // },

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
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl2.currentIndex = index;
    },
    backTopClick() {
      this.$refs.scroll.scrollTo(0, 0, 500);
    },

    contentScroll(position) {
      // console.log(position);
      // 判断backTop是否显示
      this.isShowBackTop = -position.y > 600;

      // 决定tabControl 是否吸顶
      this.isTabFixed = -position.y > this.tabOffsetTop;
    },

    loadMore() {
      // console.log('sjagsadsas');
      this.getHomeGoods(this.currentType);
      this.$refs.scroll.refresh();
    },

    /**
     * 网络请求相关
     */
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      let page = this.goods[type].page;
      getHomeGoods(type, page).then(res => {
        // console.log(res)
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;

        //完成上拉加载更多
        this.$refs.scroll.finishPullUp();
      });
    }
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    }
  }
};
</script>

<style scoped>
#home {
  height: 100vh;
  position: relative;
}
.home-nav {
  background-color: pink;
  color: white;
  /* position: fixed;
  top: 0;
  left: 0;
  right: 0; */
  z-index: 999;
}
/* .tab-control {
  position: sticky;
  top: 43px;
  z-index: 99;
} */

.tabControl {
  position: relative;
  z-index: 99;
}
.homecontent {
  /* height: calc(100% - 93px);
  
  margin-top: 44px; */
  position: absolute;
  left: 0;
  top: 44px;
  bottom: 49px;
  overflow: hidden;
}
</style>
