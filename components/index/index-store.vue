<template>
  <div
    :style="{
      transform: `translate(${move}px)`
    }"
    class="index-store">
    Index Store {{ move }}
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component
export default class indexStore extends Vue {
  w: any = 0
  get move() {
    return (this.$parent as any).move
  }
  mounted() {
    this.w = window.innerWidth
    console.log(this.w)
  }
}
</script>
<style lang="sass" scoped>
.index-store
  min-width: 100%
  flex: 1
  min-height: 100%
  scroll-snap-align: center
  background: #f00
  position: absolute
  overflow: hidden
  z-index: 100
  left: 100%
// responsive
// @media (max-width: 812px)
</style>
