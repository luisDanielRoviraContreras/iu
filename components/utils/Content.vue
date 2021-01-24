<template>
  <transition
      name="content"
      @enter="enter"
      @leave="leave"
    >
    <div
      v-if="value"
      class="content">
      <div @click="$emit('input', false)" class="shadow"></div>
      <div
      @touchstart="onTouchStart"
      @touchend="onTouchEnd"
      @touchmove="onTouchMove"
      ref="con"
      :style="{
        transform: `translateY(${move}px)`
      }" class="con">
        <div class="con-line"></div>
        <!-- <header>
          <button @click="$emit('input', false)" class="btn-close">
            X
          </button>
        </header> -->
        <div class="con-slot">
          <slot></slot>
        </div>
      </div>
    </div>
  </transition>
</template>
<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
// import anime from 'animejs/lib/anime.min.js'
@Component
export default class Content extends Vue {
  @Prop({}) value: any
  touchStart: any = {
    x: 0,
    y: 0
  }
  move: any = 0
  expand: any = false

  enter (el: any, done: any) {
    (document.body as any).querySelector('#__layout').prepend(el)
    const h = window.innerHeight / 3
    this.move = h
    done()
  }

  leave (el: any, done: any) {
    setTimeout(() => {
      (document.body as any).querySelector('#__layout').removeChild(el)
      done()
    }, 250);
  }

  onTouchEnd() {
    console.log(this.move)
    if (this.move > window.innerHeight / 2) {
      this.$emit('input', false);
      (this.$refs.con as any).classList.remove('not-transition')
      this.move = 0
      this.expand = false
    } else if (this.move < 130) {
      this.expand = true
      // anime({
      //   targets: (this.$refs.con as any),
      //   translateY: 0,
      //   easing: 'cubicBezier(0.83, 0, 0.17, 1)',
      //   duration: 250
      // })
      setTimeout(() => {
        this.move = 0;
        (this.$refs.con as any).classList.remove('not-transition')
      }, 250);
    } else if (!this.expand) {
      // anime({
      //   targets: (this.$refs.con as any),
      //   translateY: window.innerHeight / 3,
      //   easing: 'cubicBezier(0.83, 0, 0.17, 1)',
      //   duration: 250
      // })
      setTimeout(() => {
        this.move = window.innerHeight / 3;
        (this.$refs.con as any).classList.remove('not-transition')
      }, 250);
    } else {
      this.expand = true
      // anime({
      //   targets: (this.$refs.con as any),
      //   translateY: 0,
      //   easing: 'cubicBezier(0.83, 0, 0.17, 1)',
      //   duration: 250
      // })
      setTimeout(() => {
        this.move = 0;
        (this.$refs.con as any).classList.remove('not-transition')
      }, 250);
    }
  }

  onTouchStart(e: any) {
    this.touchStart = {
      x: e.changedTouches[0].clientX,
      y: e.changedTouches[0].clientY - this.move
    }
  }

  onTouchMove (e: any) {
    const dx = e.changedTouches[0].clientY - this.touchStart.y
    console.log(dx)
    if (this.touchStart.y > 40) {
      if (Math.sign(dx) !== -1) {
        (this.$refs.con as any).classList.add('not-transition')
        this.move = dx
      }
    }
  }
}
</script>
<style lang="sass" scoped>
.con-line
  position: absolute
  top: 0px
  lef: 0px
  width: 100%
  background: transparent
  height: 23px
  z-index: 100
  top: -23px
  display: flex
  align-items: center
  justify-content: center
  &:after
    content: ''
    width: 50px
    height: 5px
    background: #fff
    position: relative
    border-radius: 5px

.content
  position: fixed
  left: 0px
  bottom: 0px
  width: 100%
  height: 100vh
  height: calc(var(--vh, 1vh) * 100)
  z-index: 10000
  transition: transform .4s cubic-bezier(0.83, 0, 0.17, 1)
  overflow: hidden

.content-enter, .content-leave-to
  .shadow
    opacity: 0
  .con
    transform: translateY(100%) !important

.shadow
  background: rgba(0,0,0,.4)
  position: absolute
  top: 0px
  width: 100%
  height: 100%
  z-index: 10
  transition: all .4s cubic-bezier(0.83, 0, 0.17, 1)

.con
  position: absolute
  left: 0px
  bottom: 0px
  width: 100%
  height: 90vh
  height: calc(var(--vh, 1vh) * 90)
  background: #ff0
  border-radius: 20px 20px 0px 0px
  // overflow: hidden
  z-index: 100
  &:not(.not-transition)
    transition: transform .4s cubic-bezier(0.83, 0, 0.17, 1)

.btn-close
  position: relative
  width: 40px
  height: 40px
// responsive
// @media (max-width: 812px)
</style>
