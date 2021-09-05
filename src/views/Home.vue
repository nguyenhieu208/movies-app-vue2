<template>
  <div class="movie-main">
    <MovieComp 
      title="This Week's Trending Movies"
      apiQuery="trending/movie/week"
      :apiKey='apiKey'
    />

    <MovieComp 
      title="Today's Trending Movies"
      apiQuery="trending/movie/day"
      :apiKey='apiKey'
    />

    <PopularActorsComp 
      title="Popular Actors"
      :apiKey='apiKey'
    />

    <MovieComp 
      title="Top Rated Movies" 
      apiQuery="movie/top_rated" 
      :apiKey='apiKey'
    />

    <ComingComp 
      title="Upcoming Movies"
      :apiKey='apiKey'
    />
    
  </div>
</template>

<script>
import MovieComp from '../components/content/MovieComp.vue';
import PopularActorsComp from '../components/content/PopularActorsComp.vue';
import ComingComp from '../components/content/ComingComp.vue';
import {apiKey} from '../apiKey/index'

export default {
  data() {
    return {
      apiKey: apiKey
    }
  },
  components: {
    MovieComp,
    PopularActorsComp,
    ComingComp
  }
}
</script>

<style lang="scss">
@import '../assets/styles/main.scss';

  .movie-main {
    background: $bg;
  }

  .movie-watch {
    background: $lightbg;

    h2 {
      color: $text;
      font-size: 2.8rem;
      font-weight: 700;

      padding: 1.4rem 0;

      @include responsive(LG) {
        font-size: 4rem;
        padding: 1.8rem 0;
      }
    }
  }

  .movie__list {
    display: flex;
    gap: 2rem;

    padding: 4rem 0;
    padding-left: 15px;
    margin-left: -15px;

    overflow-x: auto;
    overflow-y: hidden;

    @include responsive(LG) {
      gap: 3rem;
    }
  }

  ::-webkit-scrollbar {
    height: 8px;
  }

  ::-webkit-scrollbar-thumb {
    background-color: $gray;
  }

  .movie__item {
    position: relative;
    transition: all .2s linear;
    border: 3px solid transparent;


    &:hover {
      transform: scale(1.08);
      border: 3px solid $green;
    }
  }

  .movie__name,
  .movie__vote {
    color: $text;
  }

  .movie__name {
    width: 100%;

    padding: 5px;

    text-align: center;
    text-shadow: 1px 1px 0 $gray;
    font-size: 1.6rem;

    background-color: rgba(0, 0, 0, 0.2);

    position: absolute;
    top: 0;
  }

  .movie__vote {
    padding: 0.5rem;

    font-size: 1.2rem;
    background-color: rgba(0, 0, 0, 0.2);

    position: absolute;
    bottom: 8px;
    right: 8px;
  }

  .movie__date {
    color: $text;
    font-size: 1.6rem;
    text-align: center;

    padding: 5px;
    width: 100%;

    position: absolute;
    bottom: 0;
  }
</style>