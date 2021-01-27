<template>
  <div
    class="Page">
    <div
    ref="con"
    :style="{
      transform: `translateY(${move}px)`
    }" class="con">
      <header>
        <button @click="$router.go(-1)" class="btn-close">
          Atrás
        </button>
      </header>
      <slot></slot>
    </div>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import anime from 'animejs/lib/anime.min.js'
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

  mounted() {
    this.enter()
  }
}
</script>
<style lang="sass" scoped>
.Page
  position: fixed
  left: 0px
  bottom: 0px
  width: 100%
  height: 100vh
  height: calc(var(--vh, 1vh) * 100)
  z-index: 10000
  transition: transform .4s cubic-bezier(0.83, 0, 0.17, 1)
  overflow: hidden
  .con
    position: absolute
    left: 0px
    bottom: 0px
    width: 100%
    height: 100vh
    height: calc(var(--vh, 1vh) * 100)
    background: #ff0
    border-radius: 0px
  .btn-close
    position: relative
    width: 40px
    height: 40px
// responsive
// @media (max-width: 812px)
</style>
