<template>
  <div class="detail-template">
    <div 
      class="detail-main"
        :style="`background-image: radial-gradient(circle, rgba(0,0,0,0.5) 0%, #000 100%) ,url(https://image.tmdb.org/t/p/w1280${apiData.backdrop_path});`"
    >
      <div class="xo-container">
        <div class="detail-top">
          <img
            :src="`https://image.tmdb.org/t/p/w200${apiData.poster_path}`"
            :alt="apiData.title"
            :title="apiData.title"
          />

          <div class="detail__rate">
            <span class="detail__vote">{{ apiData.vote_average }}/10</span>
            <span class="detail__time">⏱ {{ apiData.runtime }} min</span>
          </div>

          <ul class="detail__genres">
            <li 
              v-for="genre in apiData.genres"
              :key="genre.id"
            >
              <a href="#">{{ genre.name }}</a>            
            </li>
          </ul>
        </div>

        <div class="detail-content">
          <div class="detail__heading">
            <h3>{{ apiData.title }}</h3>
            <span class="detail__subheading">"{{ apiData.tagline }}"</span>
          </div>
          <div class="detail__desc">
            {{ apiData.overview }}
          </div>
        </div>
      </div>

    </div>

    <div class="detail-credits">
      <div class="detail-cast xo-container">
        <h2>Cast</h2>
        <ul class="detail-cast__list xo-row">
          <li 
            class="xo-col-12 xo-col-md-6 xo-col-lg-4 xo-col-xl-3"
            v-for="user in apiData.credits.cast"
            :key="user.id"
          >
            <div class="detail-cast__item">
              <div class="detail-cast__img">
                <img v-if="user.profile_path"
                  :src="`https://image.tmdb.org/t/p/w92${user.profile_path}`"
                  :alt="user.original_name"
                  :title="user.original_name"
                />
                <img v-else
                  src="https://scontent.fhan5-7.fna.fbcdn.net/v/t1.6435-9/69133411_2381986118787345_4609580672703528960_n.jpg?_nc_cat=103&ccb=1-5&_nc_sid=09cbfe&_nc_ohc=WUYlbQwrVVUAX9nNdhj&_nc_ht=scontent.fhan5-7.fna&oh=ec6ad0f79f9982bd2f66375f67258da9&oe=615BBCDE"
                  :alt="user.original_name"
                  :title="user.original_name"
                />
              </div>
              <div class="detail-cast__info">
                <div class="detail-cast__name">{{ user.name }}</div>
                <div class="detail-cast__role">as {{ user.character }}</div>
              </div>
            </div>
            
          </li>
        </ul>
      </div>
    </div>

    <div class="detail-similar">
      <div class="detail-similar-wrapper xo-container">
        <h2>Similar Movies</h2>

        <div class="detail-similar__list xo-row">
          <div 
            class="detail-similar__item xo-col-6 xo-col-md-3 xo-col-lg-2"
            v-for="(movie, index) in apiData.similar_movies.results"
            :key="index"
          >
            <div class="detail-similar__img">
              <img
                  :src="`https://image.tmdb.org/t/p/w200${movie.poster_path}`"
                  :alt="movie.title"
                  :title="movie.title"
                />
            </div>
            <div class="detail-similar__name">
              {{ movie.title }} ({{ movie.release_date }})
            </div>
          </div>
        </div>

      </div>
    </div>

  </div>
</template>

<script>
import {apiKey} from '../apiKey/index';

export default {
  data() {
    return {
      apiData: {},
      id: this.$route.params.id,
    }
  },
  created() {
    // console.log(this.id);
    // console.log(apiKey);
    // fetch(`https://api.themoviedb.org/3/movie/436969?api_key=3b7761605b6b24f4d58f1145729f81dc&append_to_response=similar_movies,credits,external_ids`)

    fetch(`https://api.themoviedb.org/3/movie/${this.id}?api_key=${apiKey}&append_to_response=similar_movies,credits,external_ids`)
      .then((res) => res.json())
      .then(this.results) 
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    results(results) {
      this.apiData = results;
    }
  }
}
</script>

<style lang="scss">
@import '../assets/styles/main.scss';

  .detail-main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    
    min-height: 650px;
    // padding: 2rem 1rem;

    background-repeat: no-repeat;
    background-position: center 20%;
    background-size: cover;
    color: $text;
  }

  .detail-top {
    display: flex;
    flex-direction: column;
    align-items: center;

    img {
      transition: all .2s linear;
      cursor: pointer;

      &:hover {
        transform: scale(1.06);
      }
    }

    .detail__rate {
      padding: 10px 0;
    }

    span {
      font-size: 16px;
    }

    .detail__time {
      margin-left: 5px;
    }
  }

  .detail__genres {
    display: flex; 

    li {
      background: $lightbg;
      padding: 0.5rem;
      margin: 0 5px;

      transition: all 0.2s linear;
      cursor: pointer;

      &:hover {
        background: $green;
      }
    }

    a {
      font-size: 16px;
    }
  }

  /** COntent */
  .detail-content {

  }

  .detail__heading {
    padding-top: 24px;
    h3 {
      margin: 0;
      font-size: 3.2rem;
      text-shadow: #fff 0 0 5px;
    }

    .detail__subheading {
      font-size: 1.6rem;
      font-style: italic;
    }
  }

  .detail__desc{
    font-size: 1.6rem;
    padding-top: 10px;
  }

  /** Cast */
  .detail-credits{
    background: $bg;
    padding-top: 5rem;
    padding-bottom: 5rem;
  }
  .detail-cast{
    h2 {
      color: $text;
      font-weight: 600;
    }
  }
  .detail-cast__list{
    padding-top: 2rem;

    li {

    }
  }

  .detail-cast__item{
    display: flex;
    align-items: center;

    padding: 10px;
    margin-bottom: 10px;

    border-radius: 50px;

    transition: all .2s linear;

    &:hover {
      background: $green;
    }
  }

  .detail-cast__img{
    @include box(9.2rem, 9.2rem);

    img {
      @include box(9.2rem, 9.2rem);
      border-radius: 100%;
      object-fit: cover;
    }
  }
  .detail-cast__info{
    color: $text;
    font-size: 16px;
    padding-left: 10px;
  }

  .detail-cast__name{
    font-weight: 600;
  }

  .detail-cast__role{
    color: $gray;
  }

  /** similar */
  .detail-similar {
    background: $bg;

    h2 {
      color: $text;
    }
  }

  .detail-similar__list{
    padding-top: 2rem;
  }
  .xo-row{

  }
  .detail-similar__item{
    transition: all .2s linear;
    transform: scale(0.96);

    display: flex;
    flex-direction: column;
    align-items: center;

    margin-bottom: 30px;
    &:hover {
      transform: scale(1)
      // img {
      // }
    }
  }
  
  .detail-similar__img{
    @include box(100%, 100%);

    img {
      @include box(100%, 100%);
    }
  }

  .detail-similar__name{
    width: 100%;
    padding: 5px 10px;
    color: $text;
    font-size: 16px;
    background: $green;
    text-align: center;
  }
</style>