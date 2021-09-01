<template>
  <header class="header">
    <div class="xo-container header-top">
      <Logo />
      <MenuIcon />
    </div>

    <div class="header-nav">
      <div class="header-nav__list">

        <div class="header-nav__item">
          <router-link class="header-nav__link" to="#">TV Shows</router-link>
          <router-link class="header-nav__link" to="#">Movies</router-link>
          <router-link class="header-nav__link" to="#">Upcoming</router-link>
        </div>

        <div class="header-nav__item">
          <router-link class="header-nav__link" to="#">Login</router-link>
          <router-link class="header-nav__link" to="#">Register</router-link>
        </div>
      </div>

    </div>
  </header>
</template>

<script>
import Logo from '../Logo.vue';
import MenuIcon from '../header/MenuIcon.vue';

export default {
  data() {
    return {

    }
  },
  components: {
    Logo,
    MenuIcon
  }
}
</script>

<style>
  .header {
    background: #0b0f16; 
    padding: 2rem 0;
  }

  .header-top {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  /*
  * Navbar
  */
  .header-nav{

  }
  .header-nav__list{

  }
  .header-nav__item{

  }
  .header-nav__link{
    color: #fff;
  }
</style>
