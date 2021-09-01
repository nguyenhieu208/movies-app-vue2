<template>
  <div :class="[search ? 'is-active' : '' , 'header__search']">
    <form action="#">
      <input type="text" class="header__search-input" placeholder="Search...">
      <span class="header__search-icon" @click="isExpand">
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
  data() {
    return {

    }
  },
  methods: {
    isExpand() {
      this.search = false;
      this.$emit('closeSearch', this.search)
    }
  },
  component: {
  }
}
</script>

<style lang="scss" scoped>
  .header__search {
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
    height: 74px;
    width: 100%;

    display: flex;
    justify-content: center;

    input {
      background: #242424;
      width: 100%;
      height: 100%;
      padding-left: 20px;
      font-size: 18px;
      color: #fff;
      border: none;
    }

    .header__search-icon {
      // width: 100%;
      height: 100%;
      cursor: pointer;

      display: flex;
      align-items: center;
      background: #242424;
      padding: 1rem 2rem;
    }

    svg {
      // width: 100%;
      // height: 100%;
    }
  }
</style>