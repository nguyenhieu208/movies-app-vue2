<template>
  <div :class="[search ? 'is-active' : '' , 'header-search']">
    <form action="#">
      <input 
        type="text" 
        placeholder="Search..." 
        @input="handleSearch($event)"
        v-model="value"
      >
      <span class="header-search__icon" @click="isExpand">
        <svg
          width="16"
          height="16"
          viewBox="0 0 25 26"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path d="M0.736328 1.62598L23.7363 24.626" stroke="#fff" stroke-width="2" />
          <path
            d="M23.6445 1.70801L0.817893 24.5346"
            stroke="#fff"
            stroke-width="2"
          />
        </svg>
      </span>
    </form>

    <div class="test">
      <div class="header-result">
        <ul class="header-result__list">
          <li 
            class="header-result__item"
            v-for="(data, index) in datas.results"
            :key="index"
          >
            <router-link
              @click.native="isExpand"
              :to="{ name: 'detail', params: { id: data.id } }"
              class="header-result__link"
            >
              <img
                :src="`https://image.tmdb.org/t/p/w200${data.poster_path}`"
                :alt="data.title"
                :title="data.title"
              />
              <div class="header-result__content">
                <div class="header-result__name" v-if="data.title">{{ data.title }}</div>
                <div class="header-result__name" v-else>{{ data.name }}</div>
                <div class="header-result__vote">{{ data.vote_average }}/10</div>
              </div>
            </router-link>
          </li>
        </ul>
      </div>
    </div>

  </div>
</template>

<script>
import {apiKey} from '../../apiKey/index';

export default {
  props: ['search'],
  data() {
    return {
      value: '',
      datas: {},
    }
  },
  methods: {
    isExpand() {
      this.$emit('closeSearch', false);
      this.value = '';
      this.datas = {};
    },
    handleSearch(e) {
      if (e.target.value.trim()) {
        fetch(`https://api.themoviedb.org/3/search/multi?api_key=${apiKey}&query=${e.target.value}`)
          .then(async response =>  await response.json())
          .then(this.results)
          .catch(error => {
            this.errorMessage = error;
            console.error("There was an error!", error);
          });
      }
    },
    results(results) {
      this.datas = results;
    }
  }
}
</script>

<style lang="scss">
@import '../../assets/styles/main';

  .header-search {
    width: 100%;
    padding: 0;

    display: flex;
    flex-direction: column;
    align-items: center;

    z-index: 20;

    transform: translateY(-110%);
    transition: all .3s linear;

    position: fixed;
    top: 0;
    left: 0;

    &.is-active {
      transform: translateY(0);
    }
  }
  
  form {    
    @include box(100%, 7.4rem);

    display: flex;
    justify-content: center;

    input {
      @include box(100%, 100%);

      background: $gray;

      color: $text;
      font-size: 1.8rem;
      
      padding-left: 2rem;

      border: none;
    }

    .header-search__icon {
      display: flex;
      align-items: center;

      background: $gray;
      padding: 1rem 2rem;

      cursor: pointer;
    }
  }

  /** Result */
  .test {
    background: $bg;
    width: 100%;
    max-height: calc(100vh - 72px);
    overflow: scroll;
    overflow-x: hidden;
  }
  .header-result{
    padding: 0;
  }
  .header-result__list{

  }
  .header-result__item{
    padding: 15px;
    border-bottom: 1px solid $green;
  }
  .header-result__link{
    display: flex;
    align-items: center;
    img {
      @include box(8rem, 10rem);
      object-fit: cover;

      @include responsive(LG) {
        @include box(12rem, 15rem);
      }
    }
  }

  .header-result__content {
    color: $text;
    font-size: 1.6rem;
    padding-left: 20px;
  }
</style>