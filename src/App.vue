<template>
  <div id="app">
    <HeaderComp />
    <Home />
    <FooterComp />
  </div>
</template>

<script>
import HeaderComp from './components/header/HeaderComp.vue';
import Home from './views/Home.vue';
import FooterComp from './components/footer/FooterComp.vue';

export default {
  components: {
    HeaderComp,
    Home,
    FooterComp
  }
}
</script>

<style lang="scss">
</style>
