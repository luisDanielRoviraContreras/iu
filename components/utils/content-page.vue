<template>
  <div
    @touchstart="onTouchStart"
    @touchend="onTouchEnd"
    @touchmove="onTouchMove"
    class="content-page">
    <div
    ref="con"
    :style="{
      transform: `translateY(${move}px)`
    }" class="con">
      <header>
        <button @click="$router.go(-1)" class="btn-close">
          X
        </button>
      </header>
      <slot></slot>
    </div>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
// import anime from 'animejs/lib/anime.min.js'
@Component
export default class contentPage extends Vue {
  touchStart: any = {
    x: 0,
    y: 0
  }
  move: any = 0

  enter () {
    (document.body as any).querySelector('#__layout').prepend(this.$el)
  }

  onTouchEnd() {
    console.log(this.touchStart)
    if (this.move > 270) {
      this.$router.go(-1)
    } else {
      // anime({
      //   targets: this.$refs.con,
      //   translateY: 0,
      //   easing: 'cubicBezier(0.83, 0, 0.17, 1)',
      //   duration: 250
      // })
      setTimeout(() => {
        this.move = 0
      }, 250);
    }

    const scalePage: any = document.querySelector('.content-page ~ .mobile-layout')
    scalePage.style.transition = `all .25s ease`
    scalePage.style.transform = ``
  }

  onTouchStart(e: any) {
    this.touchStart = {
      x: e.changedTouches[0].clientX,
      y: e.changedTouches[0].clientY
    }
  }

  onTouchMove (e: any) {
    const dx = e.changedTouches[0].clientY - this.touchStart.y
    // console.log(dx)
    if (this.touchStart.y > 40) {
      if (Math.sign(dx) !== -1) {
        this.move = dx
        const scalePage: any = document.querySelector('.content-page ~ .mobile-layout')
        if (this.move < 500) {
          const scale = `0.9${this.move * 2 < 100 ? `0${this.move * 2 < 10 ? `0${this.move * 2}` : this.move * 2}` : this.move * 2}`
          const translate = `-${31 - this.move / 16}px`
          scalePage.style.transition = `0s`
          scalePage.style.transform = `scale(${scale}) translate(0, ${translate})`
        }
      }
    }
  }

  mounted() {
    this.enter()
  }
}
</script>
<style lang="sass">
.content-page
  position: fixed
  left: 0px
  bottom: 0px
  width: 100%
  height: 100vh
  height: calc(var(--vh, 1vh) * 100)
  z-index: 10000
  transition: transform .4s cubic-bezier(0.83, 0, 0.17, 1)
  overflow: hidden
  &:not(.page-enter):not(.page-leave-to)
    ~ .mobile-layout
      transform: scale(.9) translate(0,-31px)
      border-radius: 14px 14px 0px 0px !important
      .mobileNavbar
        border-radius: 14px 14px 0px 0px !important
.mobile-layout
  transition: transform .5s cubic-bezier(0.83, 0, 0.17, 1), border-radius .25s ease
  border-radius: 0px

.con
  position: absolute
  left: 0px
  bottom: 0px
  width: 100%
  height: 97vh
  height: calc(var(--vh, 1vh) * 97)
  background: #ff0
  border-radius: 20px 20px 0px 0px
  overflow: hidden

.btn-close
  position: relative
  width: 40px
  height: 40px
// responsive
// @media (max-width: 812px)
</style>
