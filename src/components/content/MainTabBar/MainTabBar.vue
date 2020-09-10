<template>
  <tab-bar>
    <tab-bar-item link="/home" activeColor="pink">
      <template v-slot:item-icon>
        <img  src="../../../assets/img/tabbar/home.svg" alt="" />
      </template>
      <template v-slot:item-icon-active>
        <img  src="../../../assets/img/tabbar/home_active.svg" alt=""/>
      </template>
      <template v-slot:item-text>首页</template>
    </tab-bar-item>

    <tab-bar-item link="/category" activeColor="pink">
      <template v-slot:item-icon>
        <img  src="../../../assets/img/tabbar/category.svg" alt="" />
      </template>
      <template v-slot:item-icon-active>
        <img  src="../../../assets/img/tabbar/category_active.svg" alt=""/>
      </template>
      <template v-slot:item-text>首页</template>
    </tab-bar-item>

    <tab-bar-item link="/cart" activeColor="pink">
      <template v-slot:item-icon>
        <img  src="../../../assets/img/tabbar/cart.svg" alt="" />
      </template>
      <template v-slot:item-icon-active>
        <img  src="../../../assets/img/tabbar/cart_active.svg" alt=""/>
      </template>
      <template v-slot:item-text>首页</template>
    </tab-bar-item>

    <tab-bar-item link="/profile" activeColor="pink">
      <template v-slot:item-icon>
        <img  src="../../../assets/img/tabbar/profile.svg" alt="" />
      </template>
      <template v-slot:item-icon-active>
        <img  src="../../../assets/img/tabbar/profile_active.svg" alt=""/>
      </template>
      <template v-slot:item-text>首页</template>
    </tab-bar-item>
  </tab-bar>
</template>

<script>
import TabBar from '../../tabbar/TabBar'
import TabBarItem from '../../tabbar/TabBarItem'

export default {
  name: "MainTabBar",
  components: {
    TabBar,
    TabBarItem
  }
};
</script>

<style></style>
