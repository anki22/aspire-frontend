<script setup>
const menu = [
  {
    title: "Home",
    class: "home",
  },
  {
    title: "Cards",
    class: "cards active",
  },
  {
    title: "Payments",
    class: "payments",
  },
  {
    title: "Credit",
    class: "credit",
  },
  {
    title: "Profile",
    class: "profile",
  }
]
</script>

<template>
  <div class="menu">
    <div v-for="(item, index) in menu" :key="index" class="menu-item" :class="item.class">
      <span class="icon"></span>
      <span>{{ item.title }}</span>
    </div>
  </div>
</template>

<style lang="scss">
.menu {
  display: flex;
  position: fixed;
  width: 100%;
  bottom: 0;
  z-index: 1;
  background-color: #fff;
  justify-content: space-around;
  padding: 10px 0 8px;
  box-shadow: rgba(0, 0, 0, 0.3) 0px 4px 12px;
  .menu-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    font-size: 9px;
    color: #DDDDDD;
    &.active {
      color: #01D167;
      font-weight: 600;
    }
    &.home .icon {
      background-image: url('../assets/images/home.svg');
    }
    &.cards .icon {
      background-image: url('../assets/images/cards-active.svg');
    }
    &.payments .icon {
      background-image: url('../assets/images/payments.svg');
    }
    &.credit .icon {
      background-image: url('../assets/images/credit.svg');
    }
    &.profile .icon {
      background-image: url('../assets/images/profile.svg');
    }
  }
  .icon {
    width: 24px;
    height: 24px;
  }
  
}
</style>
