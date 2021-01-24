<template>
  <div class="mobile-layout">
    <mobile-navbar />
    <Nuxt />
    <mobile-footer-bar />
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component
export default class mobileLayout extends Vue {
  setHeight() {
    const vh = window.innerHeight * 0.01
    document.documentElement.style.setProperty('--vh', `${vh}px`)
    setTimeout(function () {
      window.scrollTo(0, 1)
    }, 0)
  }

  mounted () {
    this.setHeight()
    window.addEventListener('resize', this.setHeight);
  }
}
</script>
<style lang="sass" scoped>
.mobile-layout
  height: calc(var(--vh, 1vh) * 100)
  display: flex
  align-items: flex-start
  justify-content: flex-start
  flex-direction: column
  overflow: hidden
  .page
    flex: 1
    width: 100%
    overflow: auto
// responsive
// @media (max-width: 812px)
</style>
