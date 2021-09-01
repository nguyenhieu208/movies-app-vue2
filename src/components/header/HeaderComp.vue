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
          :class="[search ? 'is-active' : '', 'header__overlay']" 
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

<style lang="scss" scoped>
@import '../../assets/styles/utils/mixins/responsive';

  .header {
    background: #0b0f16; 
    @include responsive(LG) {
      display: flex;
    }
  }

  .header-top {
    padding-top: 2rem;
    padding-bottom: 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  @include responsive(LG) {
    .header__icon {
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
    background: #0b0f16;
    width: 100%;
    height: calc(100vh - 72px);
    position: fixed;
    transform: translateX(100%);
    transition: all .3s linear;
    opacity: 0;
    &.active {
      transform: translateX(0);
      opacity: 1;
      transition: all .3s linear;
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
    padding: 1rem;
    color: #fff;
    font-size: 20px;
    font-weight: 600;
    position: relative;

    &::after {
      content: '';
      display: block;
      position: absolute;
      background: #fff;
      width: 0;
      height: 1px;
      transition: all .2s linear;
    }

    &:hover::after {
      width: calc(100% - 18px);
    }
  }

  /*
  * Overlay
   */

  .header__overlay {
    &.is-active {
      position: fixed;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      cursor: pointer;
      background: rgba($color: #000000, $alpha: 0.2);
    }
  }
</style>
