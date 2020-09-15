<template>
  <nav-bar>
    <template #left>
      <div class="back" @click="backClick">
        <img src="~assets/img/common/back.svg" alt="" />
      </div>
    </template>
    <template #center>
      <div class="title">
        <div
          v-for="(item, index) in details"
          :key="index"
          class="title-item"
          :class="{ active: index === currentIndex }"
          @click="itemClick(index)"
        >
          {{ item }}
        </div>
      </div>
    </template>
  </nav-bar>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";

export default {
  name: "DetailNavBar",
  components: {
    NavBar
  },
  data() {
    return {
      details: ["商品", "参数", "评论", "推荐"],
      currentIndex: 0
    };
  },
  methods: {
    itemClick(index) {
      this.currentIndex = index;
    },
    backClick() {
      this.$router.back();
    }
  }
};
</script>

<style scoped>
.title {
  display: flex;
}
.title-item {
  font-weight: normal;
  font-size: 18px;
  flex: 1;
}
.active {
  color: pink;
}
.back img {
  margin-top: 12px;
}
</style>
