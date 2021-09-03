<template>
  <div :class="[search ? 'is-active' : '' , 'header-search']">
    <form action="#">
      <input type="text" placeholder="Search...">
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
  </div>
</template>

<script>

export default {
  props: ['search'],
  methods: {
    isExpand() {
      this.search = false;
      this.$emit('closeSearch', this.search)
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
      
      padding-left: 20px;

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
</style>