<template>
  <div id="app">
    <HeaderComp />
    <div class="xo-container">
      <MovieComp />
    </div>
    <FooterComp />
  </div>
</template>

<script>
import HeaderComp from './components/header/HeaderComp.vue';
import MovieComp from './components/content/MovieComp.vue'
import FooterComp from './components/footer/FooterComp.vue';

export default {
  data() {
    return {
      name: 'HIei'
    }
  },
  components: {
    HeaderComp,
    MovieComp,
    FooterComp
  }
}
</script>

<style lang="scss">

</style>
