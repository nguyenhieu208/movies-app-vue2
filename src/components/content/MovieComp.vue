<template>
  <div class="movie-watch">
    <div class="xo-container">
      <h2>{{ title }}</h2>
      <div class="movie__list">
        
        <router-link
          v-for="(data, index) in datas.results"
          :key="index"
          :to="{ name: 'detail', params: { id: data.id } }"
          class="movie__item"
        >
          <img
            :src="`https://image.tmdb.org/t/p/w200${data.poster_path}`"
            :alt="data.title"
            :title="data.title"
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
  props: ['title', 'apiQuery', 'apiKey'],
  data() {
    return {
      datas: {}
    }
  },
  created() {
    fetch(`https://api.themoviedb.org/3/${this.apiQuery}?api_key=${this.apiKey}`)
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
  .movie-watch {
    margin-bottom: 60px;
  }
</style>