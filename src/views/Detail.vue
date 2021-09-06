<template>
  <div class="detail-template">
    <div 
      class="detail-main"
        :style="`background-image: radial-gradient(circle, rgba(0,0,0,0.5) 0%, #000 100%) ,url(https://image.tmdb.org/t/p/w1280${apiData.backdrop_path});`"
    >
      <div class="xo-container">
        <div class="xo-row">
          <div class="detail-top xo-col-md-4 xo-col-lg-3">
            <a 
              :href="`https://image.tmdb.org/t/p/original${apiData.poster_path}`"
              target="_blank"
            >
              <img
                :src="`https://image.tmdb.org/t/p/w200${apiData.poster_path}`"
                :alt="apiData.title"
                :title="apiData.title"
              />
            </a>

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

          <div class="detail-content xo-col-md-8 xo-col-lg-5">
            <div class="detail__heading">
              <h3>{{ apiData.title }}</h3>
              <span class="detail__subheading">"{{ apiData.tagline }}"</span>
            </div>
            <div class="detail__desc">
              {{ apiData.overview }}
            </div>
            <div class="detail__socials">
              <a
                v-if="apiData.homepage"
                :href="`${apiData.homepage}`"
                class="hero__social"
                target="_blank"
                :title="apiData.homepage"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  class="hero__social-icon"
                >
                  <path
                    fill="#fff"
                    d="M21 13v10h-6v-6h-6v6h-6v-10h-3l12-12 12 12h-3zm-1-5.907v-5.093h-3v2.093l3 3z"
                  />
                </svg>
              </a>

              <a
                v-if="apiData.external_ids.imdb_id"
                :href="`https://imdb.com/title/${apiData.external_ids.imdb_id}`"
                target="_blank"
                class="hero__social"
                alt="IMDB"
                title="IMDB"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="hero__social-icon"
                  viewBox="0 0 24 24"
                >
                  <defs />
                  <path
                    fill="#fff"
                    d="M22.4 0H1.6C.7 0 .1.7 0 1.6v20.8c0 .9.7 1.5 1.6 1.6h20.8c1 0 1.6-.8 1.6-1.7V1.7c0-.9-.7-1.6-1.6-1.7zm0 .5a1.2 1.2 0 011.1 1.2v20.6c0 .6-.5 1.1-1.1 1.2H1.6c-.6 0-1-.5-1.1-1.1V1.6C.5 1 1 .6 1.6.5h20.8zM4.8 8.3v7.3h-2V8.3h2zm6.5 0v7.3H9.7v-5l-.7 5H7.8l-.7-4.8v4.8H5.4V8.3H8l.2 1.5.3 1.9.5-3.4h2.4zm3 1.3l.2.2v3.5l-.1.9c0 .1-.2.2-.5.2V9.5h.4zm0 6h1l.6-.3.3-.5.1-1.4V11 9.5l-.4-.7c-.1-.2-.4-.3-.7-.4a8 8 0 00-1.8-.1H12v7.3h2.3zm5.1-1.8v.7l-.3.2c-.1 0-.2 0-.3-.2V12v-.6l.3-.1.3.1V14zM17 8.3v7.3h1.7v-.4l.6.4.7.1c.3 0 .5 0 .8-.2l.4-.6v-3-.9l-.1-.4a1 1 0 00-.5-.4H20a2 2 0 00-.7 0l-.5.5V8.3H17z"
                  />
                </svg>
              </a>

              <a
                v-if="apiData.external_ids.facebook_id"
                :href="`https://facebook.com/${apiData.external_ids.facebook_id}`"
                target="_blank"
                class="hero__social"
                alt="Facebook"
                title="Facebook"
              >
                <svg xmlns="http://www.w3.org/2000/svg" class="hero__social-icon" viewBox="0 0 24 24" data-v-74779916=""><defs data-v-74779916=""></defs><path fill="#fff" d="M24 12a12 12 0 10-14 12v-8H7v-4h3V9c0-3 2-4 5-4h2v3h-1c-2 0-2 1-2 2v2h3v4h-3v8c6-1 10-6 10-12z" data-v-74779916=""></path></svg>
              </a>

              <a
                v-if="apiData.external_ids.twitter_id"
                :href="`https://twitter.com/${apiData.external_ids.twitter_id}`"
                target="_blank"
                class="hero__social"
                alt="Twitter"
                title="Twitter"
              >
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" data-v-74779916=""><defs data-v-74779916=""></defs><path fill="#fff" d="M24 4.6a10 10 0 01-2.9.7 5 5 0 002.2-2.7c-1 .6-2 1-3.1 1.2a5 5 0 00-8.4 4.5A14 14 0 011.6 3.2 4.8 4.8 0 001 5.6a5 5 0 002.2 4.1 4.9 4.9 0 01-2.3-.6A5 5 0 005 14a5 5 0 01-2.2 0 5 5 0 004.6 3.5 9.9 9.9 0 01-6.1 2.1H0a14 14 0 007.6 2.2c9 0 14-7.5 14-14V7A10 10 0 0024 4.6z" data-v-74779916=""></path></svg>
              </a>

              <a
                v-if="apiData.external_ids.instagram_id"
                :href="`https://instagram.com/${apiData.external_ids.instagram_id}`"
                target="_blank"
                class="hero__social"
                alt="Instagram"
                title="Instagram"
              >
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" data-v-74779916=""><defs data-v-74779916=""></defs><path fill="#fff" d="M12 0H7C5.9.2 5 .4 4.2.7c-.7.3-1.4.7-2 1.4S.8 3.4.5 4.1c-.3.8-.5 1.7-.5 3a83.6 83.6 0 00.5 12.8c.3.7.7 1.4 1.4 2 .7.8 1.3 1.2 2.1 1.5.8.3 1.7.5 3 .5a83.6 83.6 0 0012.8-.5c.7-.3 1.4-.7 2-1.4.8-.7 1.2-1.3 1.5-2.1.3-.8.5-1.7.5-3a83.6 83.6 0 00-.5-12.8c-.3-.7-.7-1.4-1.4-2-.7-.8-1.3-1.2-2.1-1.5-.8-.3-1.7-.5-3-.5L12 0zm0 2.2h4.8c1.2 0 1.9.3 2.3.4.5.3 1 .5 1.4 1 .4.4.6.8.9 1.3.1.4.3 1 .4 2.2a84 84 0 01-.5 12c-.2.5-.4 1-.9 1.4-.4.4-.8.6-1.3.9-.5.1-1.1.3-2.3.4a84.5 84.5 0 01-12-.5c-.5-.2-.9-.4-1.3-.9-.4-.4-.7-.8-.9-1.3-.2-.5-.4-1.1-.4-2.3V12 7c0-1.1.2-1.8.4-2.2.2-.6.5-1 .9-1.4.4-.4.8-.7 1.4-.9.4-.2 1-.3 2.2-.4H12zm0 3.6a6.2 6.2 0 100 12.4 6.2 6.2 0 000-12.4zM12 16a4 4 0 110-8 4 4 0 010 8zm7.8-10.4a1.4 1.4 0 11-2.8 0 1.4 1.4 0 012.8 0z" data-v-74779916=""></path></svg>
              </a>
            </div>
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
            v-for="user in apiData.credits.cast.slice(0, 12)"
            :key="user.id"
          >
            <div class="detail-cast__item">
              <div class="detail-cast__img">
                <a v-if="user.profile_path"
                  :href="`https://image.tmdb.org/t/p/original${user.profile_path}`"
                  target="_blank"
                >
                  <img
                    :src="`https://image.tmdb.org/t/p/w92${user.profile_path}`"
                    :alt="user.original_name"
                    :title="user.original_name"
                  />
                </a>
                <a v-else
                  href="https://scontent.fhan5-7.fna.fbcdn.net/v/t1.6435-9/69133411_2381986118787345_4609580672703528960_n.jpg?_nc_cat=103&ccb=1-5&_nc_sid=09cbfe&_nc_ohc=WUYlbQwrVVUAX9nNdhj&_nc_ht=scontent.fhan5-7.fna&oh=ec6ad0f79f9982bd2f66375f67258da9&oe=615BBCDE"
                  target="_blank"
                >
                  <img
                    src="https://scontent.fhan5-7.fna.fbcdn.net/v/t1.6435-9/69133411_2381986118787345_4609580672703528960_n.jpg?_nc_cat=103&ccb=1-5&_nc_sid=09cbfe&_nc_ohc=WUYlbQwrVVUAX9nNdhj&_nc_ht=scontent.fhan5-7.fna&oh=ec6ad0f79f9982bd2f66375f67258da9&oe=615BBCDE"
                    :alt="user.original_name"
                    :title="user.original_name"
                  />
                </a>
              </div>
              <div class="detail-cast__info">
                <a 
                  :href="`https://www.themoviedb.org/person/${ user.id }`" 
                  class="detail-cast__name"
                  target="_blank"
                >
                  {{ user.name }}
                </a>
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
          <a
            class="detail-similar__item xo-col-6 xo-col-md-3 xo-col-lg-2"
            v-for="(movie, index) in apiData.similar_movies.results.slice(0, 18)"
            :key="index"
            :href="`${movie.id}`"
          >
            <div class="detail-similar__img">
              <img
                  :src="`https://image.tmdb.org/t/p/w200${movie.poster_path}`"
                  :alt="movie.title"
                  :title="movie.title"
                />
            </div>
            <div class="detail-similar__name">
              {{ movie.title }} ({{ movie.release_date.slice(0, 4) }})
            </div>
          </a>
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
    
    min-height: 65rem;

    background-repeat: no-repeat;
    background-position: center 20%;
    background-size: cover;
    color: $text;

    .xo-row {
      @include responsive(LG) {
        justify-content: center;
      }
    }
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
      padding: 1rem 0;
    }

    span {
      font-size: 1.6rem;
    }

    .detail__time {
      margin-left: 0.5rem;
    }
  }

  .detail__genres {
    display: flex; 
    flex-wrap: wrap;
    justify-content: center;

    li {
      background: $lightbg;
      padding: 0.5rem;
      margin: 0 0.5rem;

      transition: all 0.2s linear;
      cursor: pointer;

      @include responsive(MD) {
        padding: 0.5rem 1rem;
        margin: 0.5rem;
      }

      &:hover {
        background: $green;
      }
    }

    a {
      font-size: 1.6rem;
    }
  }

  /** COntent */
  .detail-content {
    @include responsive(MD) {
      display: flex;
      flex-direction: column;
      justify-content: center;
    }
  }

  .detail__heading {
    padding-top: 2.4rem;
    h3 {
      margin: 0;
      font-size: 3.2rem;
      text-shadow: #fff 0 0 0.5rem;

      @include responsive(MD) {
        font-size: 4.8rem;
        font-weight: 800;
      }
    }

    .detail__subheading {
      font-size: 1.6rem;
      font-style: italic;
      @include responsive(MD) {
        font-size: 1.8rem;
      }
    }
  }

  .detail__desc{
    font-size: 1.6rem;
    padding-top: 1rem;
    @include responsive(MD) {
      font-size: 2rem;
    }
  }

  .detail__socials {
    display: flex;
    margin: 1.6rem 0;

    a {
      margin-right: 0.8rem;
      svg {
        @include box(3rem, 3rem);
      }
    }
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

    padding: 1rem;
    margin-bottom: 1rem;

    border-radius: 5rem;

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
    font-size: 1.6rem;
    padding-left: 1rem;
  }

  .detail-cast__name{
    font-weight: 600;
    &:hover {
      text-decoration: underline
    }
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

  .detail-similar__item{
    transition: all .2s linear;
    transform: scale(0.96);

    display: flex;
    flex-direction: column;
    align-items: center;

    margin-bottom: 3rem;
    &:hover {
      transform: scale(1);
    }
  }
  
  .detail-similar__img{
    @include box(100%, 100%);

    img {
      @include box(100%, 100%);
      object-fit: cover;
    }
  }

  .detail-similar__name{
    width: 100%;
    padding: 0.5rem 1rem;
    color: $text;
    font-size: 1.6rem;
    background: $green;
    text-align: center;
  }
</style>