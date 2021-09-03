<template>
  <div class="popular-actors">
    <div class="xo-container">
      <h2>{{ title }}</h2>
      <ul class="xo-row popular-actors__list">
        <li 
          class="xo-col-6 xo-col-md-4 xo-col-lg-3 xo-col-xl-2 popular-actor__item"
          v-for="(data, index) in datas.results"
          :key="index"
        >
          <a
            href="#"
            class="popular-actor__link"
          >
            <span class="popular-actor__img" :style="`background-image: url(https://image.tmdb.org/t/p/w200${data.profile_path})`"></span>
            <span class="popular-actor__name" style="color: white">{{ data.name }}</span>
          </a>

        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ['title'],
  data() {
    return {
      datas: {}
    }
  },
  created() {
    fetch(`https://api.themoviedb.org/3/person/popular?api_key=3b7761605b6b24f4d58f1145729f81dc`)
      .then((res) => res.json())
      .then(this.results) 
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    results(results) {
      this.datas = results;
      console.log(results);
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../../assets/styles/utils/mixins/responsive';

  .popular-actors {
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
  .popular-actors__list{
    display: flex;
    padding-bottom: 50px;

    @include responsive(MD) {
      padding-bottom: 80px;
    }

    &.xo-row {
      margin: 0;
    }
  }

  .popular-actors__item{
    padding: 0;
  }
  .popular-actor__link{
    transition: all .2s linear;
    display: flex;
    align-items: center;
    margin: 0.25rem;
    padding: 0.5rem;
    background: #404040;
    border-radius: 0.25rem;

    &:hover {
      background: #353535;
    }

    @include responsive(MD) {
      margin: 0.5rem;
    }
  }


  .popular-actor__img {
    width: 50px;
    height: 50px;
    margin-right: 0.5rem;
    padding: 0.5rem;
    background: green;
    background-position: center 20%;
    background-size: 100%;
    border-radius: 100%;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
  }
  .popular-actor__name{
    font-size: 16px;
  }
</style>