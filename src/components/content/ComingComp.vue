<template>
  <div class="movie-watch upcoming-movie">
    <div class="xo-container">
      <h2>{{ title }}</h2>
      <div class="movie__list">
        <router-link
          to="#"
          class="movie__item"
          v-for="(data, index) in datas.results"
          :key="index"
        >
          <img
            :src="`https://image.tmdb.org/t/p/w200${data.poster_path}`"
            :alt="data.title"
            :title="data.title"
            class="movie__poster"
          />
          <div class="movie__name">{{ index + 1 }}. {{ data.title }}</div>
          <div class="movie__date">{{ data.release_date }}</div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['title', 'apiKey'],
  data() {
    return {
      datas: {}
    }
  },
  created() {
    fetch(`https://api.themoviedb.org/3/movie/upcoming?api_key=${this.apiKey}`)
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

<style lang="scss">
@import '../../assets/styles/main.scss';
  .upcoming-movie {
    background: $bg !important;

    padding-bottom: 1rem;
  }
</style>