<template>
  <div class="mobile-container" ref="container">
    <div class="mobile-content" ref="demo">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';

export default {
  computed: {
    visible() {
      return ['/'].indexOf(this.$route.path) < 0;
    }
  },

  data() {
    return {
      isFooterFixed: false
    };
  },

  mounted() {
    this.computeFooterFixed();
  },

  watch: {
    '$route.path': function(val) {
      Vue.nextTick(() => {
        this.computeFooterFixed();
      });
    }
  },

  methods: {
    computeFooterFixed() {
      if (this.$refs.container) {
        const demoSize = this.$refs.demo.getBoundingClientRect();
        const containerSize = this.$refs.container.getBoundingClientRect();
        if (demoSize.height < containerSize.height - 54) {
          this.isFooterFixed = true;
          return;
        }
      }
      this.isFooterFixed = false;
    }
  }
};
</script>

<style>

  body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td, iframe {
    margin: 0;
    padding: 0;
  }

  img, article, aside, details, figcaption, figure, footer, header, menu, nav, section, summary, time, mark, audio, video {
    display: block;
    margin: 0;
    padding: 0;
  }

  a {
    color: #4078c0;
    text-decoration: none;
  }

  body, html {
    height: 100%;
  }

  body {
    font-family: 'Helvetica Neue',Helvetica,'PingFang SC','Hiragino Sans GB','Microsoft YaHei',SimSun,sans-serif;
  }

  .mobile-container {
    height: 100%;
    overflow: auto;
    background: #f8f8f8;
    position: relative;
    -webkit-overflow-scrolling: touch;
  }

  .page-back {
    display: inline-block;
    position: absolute;
    top: 12px;
    left: 10px;
    width: 40px;
    height: 40px;
    text-align: center;
    color: #333;
    transform: rotate(180deg);

    i {
      font-size: 24px;
      line-height: 40px;
    }
  }

  .demo-title {
    font-size: 16px;
    display: block;
    line-height: 1;
    padding: 20px 15px 0;
  }

  .demo-sub-title {
    font-size: 14px;
    font-weight: normal;
    color: #999;
    padding: 30px 5px 10px;
  }

  .footer {
    margin-top: 30px;
    width: 100%;
    padding: 10px 0 20px;
    background: #f8f8f8;

    &.footer-fixed {
      position: absolute;
      bottom: 0;
      left: 0;
    }
  }
</style>
