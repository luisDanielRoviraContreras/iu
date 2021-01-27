<template>
  <Tab>
    Contenido aquí
    <input ref="input" type="text">
  </Tab>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component
export default class search extends Vue {
  mounted() {
    (this.$refs.input as any).focus()
  }
}
</script>
<style lang="sass" scoped>
// responsive
// @media (max-width: 812px)
</style>
