<template>
  <div class="mobileNavbar">
    <button @click="$route.query.back ? $router.push($route.query.back) : $router.go(-1)">
      back
    </button>
    <h4>
      Mensajes
    </h4>
    <button @click="openConfig = !openConfig">config</button>
    <Dialog v-model="openConfig">
      hola mundo
    </Dialog>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component
export default class mobileNavbar extends Vue {
  openConfig: boolean = false
}
</script>
<style lang="sass" scoped>
.mobileNavbar
  width: 100%
  position: relative
  padding: 20px
  display: flex
  align-items: center
  justify-content: space-between
  z-index: 9000
  background: #f00
  transition: all .25s ease
// responsive
// @media (max-width: 812px)
</style>
