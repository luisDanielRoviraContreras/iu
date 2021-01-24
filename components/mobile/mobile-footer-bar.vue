<template>
  <div class="mobileNavbar">
    footer bar
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component
export default class mobileNavbar extends Vue {}
</script>
<style lang="sass" scoped>
.mobileNavbar
  width: 100%
  position: relative
  padding: 20px
  background: #0f0
  z-index: 9000
// responsive
// @media (max-width: 812px)
</style>
