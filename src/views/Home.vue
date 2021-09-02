<template>
  <div class="movie-container">
    <!-- <div class="xo-container"> -->
      <MovieComp 
        title="This Week's Trending Movies"
        apiQuery="trending/movie/week"
      />

      <MovieComp 
        title="Today's Trending Movies"
        apiQuery="trending/movie/day"
      />

      <MovieComp 
        title="Top Rated Movies" 
        apiQuery="movie/top_rated" 
      />

    <!-- </div> -->
  </div>
</template>

<script>
import MovieComp from '../components/content/MovieComp.vue';

export default {
  data() {
    return {

    }
  },
  components: {
    MovieComp
  }
}
</script>

<style lang="scss" scoped>
  .movie-container {
    background: #0b0f16;
  }
</style>