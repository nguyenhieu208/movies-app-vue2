<template>
  <header class="header">
    <div class="xo-container">
      <div class="xo-row">
        <div class="header-top xo-col-12 xo-col-lg-4">
          <Logo />
          <MenuIcon 
            @toggleMenu="toggleMenu" 
            :search="search" 
            :activeIcon="activeIcon" 
          />

        </div>

        <div class="header-nav xo-col-12 xo-col-lg-8">
          <div :class="[ togglemenu ? 'active': '', 'header-nav__list xo-row']">

            <div class="header-nav__item">
              <router-link class="header-nav__link" to="#">TV Shows</router-link>
              <router-link class="header-nav__link" to="#">Movies</router-link>
              <router-link class="header-nav__link" to="#">Upcoming</router-link>
            </div>

            <div class="header-nav__item">
              <router-link class="header-nav__link" to="#">Login</router-link>
              <router-link class="header-nav__link" to="#">Register</router-link>
              <a href="#" class="header-nav__link" @click="openSearch">Search</a>
            </div>

          </div>
        </div>

        <div 
          :class="[search ? 'is-active' : '', 'header-overlay']" 
          @click="search=false">
        </div>
        
        <SearchBar :search="search" @closeSearch="closeSearch" />

      </div>
    </div>

  </header>
</template>

<script>
import Logo from '../Logo.vue';
import MenuIcon from '../header/MenuIcon.vue';
import SearchBar from './SearchBar.vue';

export default {
  data() {
    return {
      togglemenu: false,
      search: false,
      activeIcon: false
    }
  },
  methods: {
    toggleMenu() {
      this.togglemenu = !this.togglemenu;
      this.activeIcon = !this.activeIcon;
    },
    openSearch() {
      this.search = !this.search;
      this.toggleMenu();
    },
    closeSearch(search) {
      this.search = search;
    }
  },
  components: {
    Logo,
    MenuIcon,
    SearchBar
  }
}
</script>

<style lang="scss">
@import '../../assets/styles/main';

  .header {
    background: $bg; 
    @include responsive(LG) {
      display: flex;
    }
  }

  .header-top {
    padding: 2rem 0;

    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  @include responsive(LG) {
    .header-hamburger {
      display: none;
    }
  }

  /*
  * Navbar
  */
  .header-nav{
    display: flex;
    justify-content: center;

    position: relative;
  }

  .header-nav__list{
    display: flex;
    flex-direction: column;

    background: $bg;
    @include box(100%, calc(100% - 72px));

    position: fixed;

    transform: translateX(100%);
    transition: all .3s linear;

    opacity: 0;

    &.active {
      transform: translateX(0);
      opacity: 1;
      z-index: 1;
    }

    @include responsive(LG) {
      position: initial;
      top: unset;
      left: unset;

      height: unset;
      transform: unset;
      background: unset;

      opacity: 1;

      flex-direction: row;
      justify-content: space-between;
    }
  }

  .header-nav__item{
    display: flex;
    flex-direction: column;
    align-items: center;

    outline: none;

    @include responsive(LG) {
      flex-direction: row;
    }
  }

  .header-nav__link{
    color: $text;

    padding: 1rem;

    font-size: 2rem;
    font-weight: 600;

    position: relative;

    &::after {
      content: '';
      display: block;

      background: $text;
      @include box(0, 1px);

      position: absolute;

      transition: all .2s linear;
    }

    &:hover::after {
      width: calc(100% - 18px);
    }
  }

  /*
  * Overlay
   */

  .header-overlay {
    &.is-active {
      position: fixed;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;

      cursor: pointer;

      background: rgba($color: #000000, $alpha: 0.2);

      z-index: 10;
    }
  }
</style>
