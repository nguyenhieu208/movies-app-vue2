<template>
  <div class="movie-watch">
    <div class="xo-container">
      <h2>{{ title }}</h2>
      <div class="movie__list">
        
        <router-link
          v-for="(data, index) in datas.results"
          :key="index"
          to="/"
          class="movie__item"
        >
          <img
            :src="`https://image.tmdb.org/t/p/w200${data.poster_path}`"
            :alt="data.title"
            :title="data.title"
            class="movie__poster"
          />
          <div class="movie__name">{{ index + 1 }}. {{ data.title }}</div>
          <div class="movie__vote">{{ data.vote_average }}/10</div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['title', 'apiQuery'],
  data() {
    return {
      datas: {}
    }
  },
  created() {
    fetch(`https://api.themoviedb.org/3/${this.apiQuery}?api_key=3b7761605b6b24f4d58f1145729f81dc`)
      .then((res) => res.json())
      .then(this.results) 
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    results(results) {
      this.datas = results;
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../../assets/styles/utils/mixins/responsive';

  .movie-watch {
    background: #192231;
    margin-bottom: 60px;
    h2 {
      color: #fff;
      font-size: 28px;
      font-weight: 700;
      padding: 1.4rem 0;

      @include responsive(LG) {
        font-size: 40px;
        padding: 1.8rem 0;
      }
    }
  }

  .movie__list {
    display: flex;
    gap: 2rem;
    padding: 4rem 0;
    overflow-x: auto;
    overflow-y: hidden;
    padding-left: 15px;
    margin-left: -15px;

    @include responsive(LG) {
      gap: 3rem;
    }
  }

  ::-webkit-scrollbar {
      height: 8px;
    }

  ::-webkit-scrollbar-thumb {
    background-color: gray;
  }

  .movie__item {
    position: relative;
    transition: all .2s linear;

    &:hover {
      transform: scale(1.08);
    }
  }

  .movie__name,
  .movie__vote {
    color: white;
  }

  .movie__name {
    width: 100%;
    padding: 5px;
    text-align: center;
    text-shadow: 1px 1px 0 #404040;
    background-color: rgba(0, 0, 0, 0.2);
    position: absolute;
    top: 0;
  }

  .movie__vote {
    padding: 5px;
    font-size: 12px;
    background-color: rgba(0, 0, 0, 0.2);
    position: absolute;
    bottom: 8px;
    right: 8px;
  }
</style>