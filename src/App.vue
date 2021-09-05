<template>
  <div id="app">
    <HeaderComp />
    <router-view></router-view>
    <FooterComp />
  </div>
</template>

<script>
import HeaderComp from './components/header/HeaderComp.vue';
import FooterComp from './components/footer/FooterComp.vue';

export default {
  components: {
    HeaderComp,
    FooterComp
  }
}
</script>

<style lang="scss">
</style>
