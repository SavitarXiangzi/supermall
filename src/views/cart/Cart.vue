<template>
  <h2>购物车车</h2>
</template>

<script>
import { Swiper, SwiperSlide } from "vue-awesome-swiper";
import "swiper/dist/css/swiper.css";

// Vue.use(VueAwesomeSwiper, /* { default options with global component } */)

export default {
  name: "Cart",
  components: {
    Swiper,
    SwiperSlide
  },
  data() {
    return {
      banners: [ '/1.jpg', '/2.jpg', '/3.jpg' ],
      swiperOption: {
        el: '.swiper-pagination',
        autoplay: 3000,
        loop: true
      }
    };
  }
  // computed: {
  //   swiper() {
  //     return this.$refs.mySwiper.swiper;
  //   }
  // },
  // mounted() {
  //   // current swiper instance
  //   // 然后你就可以使用当前上下文内的swiper对象去做你想做的事了
  //   console.log("this is current swiper instance object", this.swiper);
  //   this.swiper.slideTo(3, 1000, false);
  // }
};
</script>

<style scoped>

</style>


