<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive"><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :style="activeStyle"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
export default {
  name: "TabBarItem",
  props: {
    link: String,
    activeColor:{
      type:String,
      default:'red'
    }
  },
  computed: {
    isActive() {
      return this.$route.path.indexOf(this.link) !== -1
    },
    activeStyle(){
      return this.isActive ? {'color': this.activeColor} : {}
    }
  },
  methods: {
    itemClick() {
      if(this.$route.path!=this.link){
        this.$router.replace(this.link)
      }
      return
      // console.log('route.path'+this.$route.path)
      // console.log('link'+this.link);
    }
  }
};
</script>

<style scoped>
.tab-bar-item{
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 14px;
}
.tab-bar-item img{
  height: 25px;
  width: 25px;
  margin-top: 3px;
  vertical-align: middle; /* 去除图片下面空白 */
  margin-bottom: 2px;
}
</style>
