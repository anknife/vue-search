<template>
  <div class="main-logo">
    <img :src="logos[selectedNow].imgSrc" @click="logoSelect" />
    <transition name="logofade">
      <ul v-show="logoListFlag&&mouseLeaveFlag" class="logoList" @mouseleave="mouseLeaveList">
        <li v-for="(item, index) in logos"
            @mouseover="logoHover(index)"
            :class="{selectback:index==logoNow}"
            @click="logoSelected(index)">
          <img :src="item.imgSrc">
        </li>
      </ul>
    </transition>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        selectedNow: 1,
        logoNow: -1,
        logoListFlag: false,
        mouseLeaveFlag: false,
        logos: [{
          imgSrc: require('../assets/360_logo.png')
        }, {
          imgSrc: require('../assets/baidu_logo.png')
        }, {
          imgSrc: require('../assets/sougou_logo.png')
        }]
      }
    },
    methods: {
      logoSelect () {
        this.logoListFlag = !this.logoListFlag
        this.mouseLeaveFlag = true
      },
      logoHover (index) {
        this.logoNow = index
      },
      logoSelected (index) {
        this.selectedNow = index
        this.logoListFlag = false
        this.$emit('getIndex', this.selectedNow)
      },
      mouseLeaveList () {
        this.mouseLeaveFlag = false
        this.logoListFlag = false
      }
    }
  }
</script>

<style>
  ul{
    list-style: none;
    padding: 0;
    margin: 0
  }

  .main-logo {
    width: 600px;
    height: 140px;
    position: relative;
    left: 50%;
    margin-left: -300px;
  }

  .main-logo img {
    display: block;
    margin: 0 auto;
    user-select: none;
    cursor: pointer;
  }

  .logoList {
    position: absolute;
    top: 100%;
    width: 200px;
    left: 50%;
    margin-left: -100px;
    z-index: 9999;
    border: 1px solid #d4d4d4;
  }

  .logoList li {
    width: 100%;
    height: 80px;
    background-color: #FEFEFE;
    line-height: 80px;
    padding-top: 1px;
  }

  .logoList li img {
    width: 100%;
    margin-top: 10px;
  }

  .logofade-enter-active,
  .logofade-leave-active {
    transition: all  .5s;
  }

  .logofade-enter,
  .logofade-leave-active {
    opacity: 0;
    transform: translateY(20px);
  }
  .selectback{
    background-color: #eee !important;
    cursor: pointer
  }
</style>
