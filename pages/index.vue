<template>
  <div
    @touchstart="onTouchStart"
    @touchend="onTouchEnd"
    @touchmove="onTouchMove"
    class="index page" :class="{ smooth }">
    <index-store />
    <index-chat />
    <index-wallet />
    <nuxt-child />
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component({
  layout (context: any) {
    return context.isMobile ? 'mobile' : 'default'
  }
})
export default class index extends Vue {
  smooth: any = false
  scrollLeft: any = 0
  touchStart: any = {
    x: 0,
    y: 0
  }
  move: any = 0

  onTouchStart(e: any) {
    this.touchStart = {
      x: e.changedTouches[0].clientX - this.move,
      y: e.changedTouches[0].clientY
    }
    console.log(this.touchStart)
  }
  onTouchEnd(e: any) {
    this.smooth = true
    if (this.move > window.innerWidth / 2) {
      this.move = window.innerWidth
    }
    if (this.move < -window.innerWidth / 2) {
      this.move = -window.innerWidth
    }
    if (this.move <= window.innerWidth / 2 && this.move >= -window.innerWidth / 2) {
      this.move = 0
    }
    setTimeout(() => {
      this.smooth = false
    }, 250);
  }
  onTouchMove(e: any) {
    let dx = e.changedTouches[0].clientX - this.touchStart.x
    console.log(dx)
    if (dx > window.innerWidth) {
      dx = window.innerWidth
    }
    if (Math.sign(dx) == -1) {
      if (dx < -window.innerWidth) {
        dx = -window.innerWidth
      }
    }
    this.move = dx
  }
}
</script>
<style lang="sass" scoped>
.index
  background: rgba(240,20,240,1)
  position: relative
  display: flex
  align-items: flex-start
  justify-content: flex-start
  // overflow: auto
  // scroll-snap-type: x mandatory
  // -webkit-overflow-scrolling: touch
  // -ms-scroll-snap-points-x: snapInterval(0%, 100%)
  overflow: hidden !important
  &.smooth
    .index-chat
      transition: all .25s ease
    .index-wallet
      transition: all .25s ease
    .index-store
      transition: all .25s ease
  li
    padding: 20px
// responsive
// @media (max-width: 812px)
</style>
