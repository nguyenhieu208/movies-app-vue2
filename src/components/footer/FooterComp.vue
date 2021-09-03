<template>
  <footer class="footer">
    <div class="xo-container">
      <div class="xo-row">
        <div class="xo-col-4 footer__logo">
          <Logo />
        </div>
        <div class="xo-col-4 footer__text">
          <p>© VMDb 2021</p>
        </div>
        <div class="xo-col-4 footer__list">
          <div class="footer__item">
            <img :src="icons[0].facebook">
          </div>
          <div class="footer__item">
            <img :src="icons[1].instagram">
          </div>
          <div class="footer__item">
            <img :src="icons[2].twitter">
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import Logo from '../Logo.vue';
export default {
  data() {
    return {
      icons: [
        { facebook: require('../../assets/images/social-icons/facebook.svg') },
        { instagram: require('../../assets/images/social-icons/instagram.svg') },
        { twitter: require('../../assets/images/social-icons/twitter.svg') },
      ]
    }
  },
  components: {
    Logo,
  }
}
</script>

<style lang="scss" scoped>
@import '../../assets/styles/main.scss';

  .footer {
    border-top: 1px solid $gray;

    padding: 1rem 0;
    background: $bg;

    .xo-row {
      flex-direction: column;
      justify-content: center;
      align-items: center;

      @include responsive(MD) {
        flex-direction: row;
      }
    }

    .xo-col-4 {
      text-align: center;
      @include responsive(MD) {
        &:nth-child(1) {
          text-align: unset;
        }
        &:nth-child(3) {
          justify-content: flex-end;
        }
      }
    }
  }

  .footer__logo {
    img {
      height: 30px;
    }
  }

  .footer__text {
    margin: 10px 0;
    color: $text;
  }

  .footer__list {
    display: flex;
    justify-content: center;
  }

  .footer__item {
    @include box(2.4rem, 2.4rem);

    margin: 0 5px;
    cursor: pointer;

    svg {
      @include box(100%, 100%);
      fill: #fff;
    }
  }
</style>