<template>
  <div v-show="!isMobile">
    <div class="guide right">
      <div class="up">
        <em style="transform:translate(0,-3px) scale(1,2)" />
      </div>
      <div class="left">
        <em style="transform:translate(-7px,3px) rotate(-90deg) scale(1,2)" />
      </div>
      <div class="down">
        <em style="transform: translate(0,9px) rotate(180deg) scale(1,2)" />
      </div>
      <div class="right">
        <em style="transform: translate(7px,3px)rotate(90deg) scale(1,2)" />
      </div>
    </div>
    <div class="guide left">
      <p>
        <a
          href="https://github.com/cvSoldier/vue-tetris"
          rel="noopener noreferrer"
          target="_blank"
          v-bind="{title:linkTitle}"
        >{{github}}:</a>
        <br />
        <iframe
          src="https://ghbtns.com/github-btn.html?user=Binaryify&repo=vue-tetris&type=star&count=true"
          frameBorder="0"
          scrolling="0"
          width="170px"
          height="20px"
          style="transform: scale(1.68);transform-origin: center left"
        />
        <br />
        <iframe
          src="https://ghbtns.com/github-btn.html?user=Binaryify&repo=vue-tetris&type=fork&count=true"
          frameBorder="0"
          scrolling="0"
          width="170px"
          height="20px"
          style="transform: scale(1.68);transform-origin: center left"
        />
      </p>
      <div class="space">SPACE</div>
    </div>
    <div class="guide qr">
      <img
        :src="QRSrc"
        v-bind="{title:QRTitle,alt:QRCode}"
      />
    </div>
  </div>
</template>

<script>
import { i18n, lan } from '../../unit/const'
import { isMobile } from '../../unit'
export default {
  name: 'Guide',
  data() {
    return {
      isMobile: isMobile()
    }
  },
  computed: {
    linkTitle: () => i18n.linkTitle[lan],
    github: () => i18n.github[lan],
    QRCode: () => i18n.QRCode[lan],
    QRTitle: () => i18n.QRNotice[lan],
    QRSrc: () =>
      window.location.protocol +
      '//binaryify.github.io/vue-tetris/static/qr.jpeg'
  },
  mounted() {
    window.addEventListener('resize', this.resize.bind(this), true)
  },
  methods: {
    resize() {
      this.isMobile = isMobile()
    }
  }
}
</script>

<style lang="less" scoped>
.background(@from, @to) {
  background: (@from + @to)/2;
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(@from),
    to(@to)
  );
  background: -moz-linear-gradient(
    top,
    @from,
    @from
  ); // IE9使用filter背景渐变, 但因为使用了borader-radius, 所以不兼容, IE9使用中和的背景色即可
  //filter:  progid:DXImageTransform.Microsoft.gradient(startColorstr='@{from}', endColorstr='@{to}');
}

.guide {
  position: absolute;
  left: 115%;
  right: 115%;
  text-align: center;
  line-height: 1;
  white-space: nowrap;
  &.right {
    right: auto;
    bottom: 5%;
  }
  &.left {
    left: auto;
    bottom: 5%;
  }
  p {
    text-align: left;
    margin-bottom: 350px;
    opacity: 0.5;
    iframe {
      margin-top: 20px;
    }
  }
  a {
    color: #005850;
    font-size: 30px;
    position: relative;
    z-index: 1;
    cursor: alias;
    text-decoration: none;
  }
  &.qr {
    left: auto;
    top: 5%;
    width: 190px;
    height: 190px;
    opacity: 0.45;
    padding: 0 0 40px 40px;
    text-align: right;
    &:hover {
      img {
        width: 100%;
        height: 100%;
      }
    }
    img {
      width: 38px;
      height: 38px;
    }
  }
  & > div {
    width: 100px;
    height: 54px;
    background: /*#404040*/ #364d4b;
    display: inline-block;
    border-radius: 4px;
    position: relative;
    color: #acc3c1;
    font-size: 16px;
    em {
      display: block;
      width: 0;
      height: 0;
      border: 6px solid;
      border-color: transparent transparent /*#ccc*/ #acc3c1;
      position: absolute;
      top: 50%;
      left: 50%;
      margin: -9px 0 0 -6px;
    }
    &:before,
    &:after {
      content: "";
      display: block;
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      border-radius: 4px;
      box-shadow: 0 5px 10px rgba(255, 255, 255, 0.15) inset;
    }
    &:before {
      box-shadow: 0 -5px 10px rgba(0, 0, 0, 0.15) inset;
    }
  }
  .up {
    height: 60px;
    display: block;
    margin: 0 auto 2px;
  }
  .down {
    margin: 0 10px;
  }
  .space {
    left: auto;
    bottom: 5%;
    height: 80px;
    width: 400px;
    line-height: 80px;
    letter-spacing: 2px;
  }
}
</style>
