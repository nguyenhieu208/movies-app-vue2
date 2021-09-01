<template>
  <div id="app">
    <HeaderComp />
    <div class="xo-container">
      <h1>{{ name }}</h1>
    </div>
  </div>
</template>

<script>
import HeaderComp from './components/header/HeaderComp.vue';

export default {
  data() {
    return {
      name: 'HIei'
    }
  },
  components: {
    HeaderComp
  }
}
</script>

<style lang="scss">

</style>
