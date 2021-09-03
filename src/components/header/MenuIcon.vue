<template>
  <div
    :class="[activeIcon ? 'active' : '', 'header-hamburger']"
    @click="handleClick"
  >
    <div class="header-hamburger-lines">
      <div class="line"></div>
      <div class="line"></div>
      <div class="line"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['search', 'activeIcon'],
  data() {
    return {
      
    }
  },
  methods: {
    handleClick() {
      this.activeIcon = !this.activeIcon;
      this.search = false;
      this.$emit('toggleMenu');
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../../assets/styles/utils/mixins/size';

  .header-hamburger {
    @include box(3.2rem, 3.2rem);

    border: none;
    outline: none;

    cursor: pointer;

    position: relative;
  }

  /* // hamburger // */
  .header-hamburger-lines {
    position: absolute;
    top: 50%;
    left: 50%;

    @include box(3.2rem, 3.2rem);
    transform: translate(-50%, -50%);
    pointer-events: none;

    /* // line // */
    .line {
      position: absolute;
      width: 32px;
      height: 6px;
      background-color: #fff;
      border-radius: 5px;
      pointer-events: none;

      &:nth-child(1) { top: 0 }
      &:nth-child(2) { top: 11px }
      &:nth-child(3) { top: 22px }
    }
  }

  /* // ANIMATION BOUTTON B3 // */
  .header-hamburger .header-hamburger-lines {
    transition: transform 0.3s ease-in-out;
  }

  .header-hamburger.active .header-hamburger-lines {
    transition: transform 0.3s 0.3s ease-in-out;
    transform: translate(-50%, -50%) rotate(360deg);
  }

  .header-hamburger .line:nth-child(1),
  .header-hamburger .line:nth-child(3) {
    transform: rotate(0deg);
    transition: transform 0.3s ease-in-out, top 0.3s 0.3s ease-in-out;
  }

  .header-hamburger .line:nth-child(2) {
    transition: opacity 0.3s 0.3s ease-in-out;
  }

  .header-hamburger.active .line:nth-child(1) {
    top: 15px;
    transform: rotate(45deg);
    transition: top 0.3s ease-in-out, transform 0.3s 0.3s ease-in-out;
  }

  .header-hamburger.active .line:nth-child(2) {
    opacity: 0;
    transition: opacity 0.3s ease-in-out;
  }

  .header-hamburger.active .line:nth-child(3) {
    top: 15px;
    transform: rotate(-45deg);
    transition: top 0.3s ease-in-out, transform 0.3s 0.3s ease-in-out;
  }
</style>