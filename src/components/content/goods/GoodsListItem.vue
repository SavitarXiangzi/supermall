<template>
  <div class="goods" @click="goToDetail">
    <img :src="goodsItem.show.img" alt="" />
    <div class="goods-info">
      <p>{{ goodsItem.title }}</p>
      <span class="price">￥{{ goodsItem.price }}</span>
      <span class="collect">{{ goodsItem.cfav }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "GoodsListItem",
  props: {
    goodsItem: {
      type: Object,
      default() {
        return [];
      }
    }
  },
  methods: {
    goToDetail: function() {
      // 1.获取iid
      let iid = this.goodsItem.iid;

      // 2.跳转到详情页面
      // this.$router.push({ path: "/detail", query: { iid } });
      this.$router.push("/detail/" + iid);
    }
    // imageLoad () {
    //   this.$bus.$emit('itemImageLoad')
    // }
  },
  computed: {
    getImg() {
      return (
        this.goodsItem.img || this.goodsItem.image || this.goodsItem.show.img
      );
    }
  }
};
</script>

<style scoped>
.goods {
  width: 47%;
  padding-bottom: 40px;
  position: relative;
}
.goods img {
  width: 100%;
  height: 300px;
  border-radius: 5px;
}

.goods-info {
  font-size: 12px;
  position: absolute;
  bottom: 5px;
  left: 0;
  right: 0;
  overflow: hidden;
  text-align: center;
}

.goods-info p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-bottom: 3px;
}

.goods-info .price {
  color: var(--color-high-text);
  margin-right: 20px;
}

.goods-info .collect {
  position: relative;
}

.goods-info .collect::before {
  content: "";
  position: absolute;
  left: -15px;
  top: 0;
  width: 14px;
  height: 14px;
  background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
}
</style>
