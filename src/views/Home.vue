<template>
  <div class="movie-container">
    <MovieComp 
      title="This Week's Trending Movies"
      apiQuery="trending/movie/week"
    />

    <MovieComp 
      title="Today's Trending Movies"
      apiQuery="trending/movie/day"
    />

    <PopularActorsComp 
      title="Popular Actors"
    />

    <MovieComp 
      title="Top Rated Movies" 
      apiQuery="movie/top_rated" 
    />
    
  </div>
</template>

<script>
import MovieComp from '../components/content/MovieComp.vue';
import PopularActorsComp from '../components/content/PopularActorsComp.vue';

export default {
  data() {
    return {

    }
  },
  components: {
    MovieComp,
    PopularActorsComp
  }
}
</script>

<style lang="scss" scoped>
  .movie-container {
    background: #0b0f16;
  }
</style>