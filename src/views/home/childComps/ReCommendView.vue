<template>
  <div class="recommend">
    <div v-for="item in recommends" class="recommend-item">
      <a :href="item.link">
        <img :src="item.image" alt="" />
        <div>{{ item.title }}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "ReCommendView",
  props: {
      recommends: {
        type: Array,
        default() {
          return [];
        }
      }
  }
};
</script>

<style scoped>
  .recommend {
    display: flex;
    padding: 10px 0 30px 0;
    border-bottom: 10px solid #eee;

  }
  .recommend-item{
    flex: 1;
    text-align: center;
  }
  .recommend-item img{
    width: 80px;
  }
</style>
