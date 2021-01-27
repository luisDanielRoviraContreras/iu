<template>
  <div
    :style="{
      transform: `translate(${move}px)`
    }"
    class="index-wallet">
      Index wallet {{ move }}
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component
export default class indexWallet extends Vue {
  w: any = 0
  get move() {
    return (this.$parent as any).move - this.w
  }
  mounted() {
    this.w = window.innerWidth
    console.log(this.w)
  }
}
</script>
<style lang="sass" scoped>
.index-wallet
  min-width: 100%
  flex: 1
  min-height: 100%
  scroll-snap-align: center
  background: #ff0
  position: absolute
  overflow: hidden
  z-index: 100
// responsive
// @media (max-width: 812px)
</style>
