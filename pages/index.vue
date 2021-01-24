<template>
  <div class="index page">
    <button @click="$router.push('/chats/')">
      Chats
    </button>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component({
  layout (context: any) {
    return context.isMobile ? 'mobile' : 'default'
  }
})
export default class index extends Vue {}
</script>
<style lang="sass" scoped>
.index
  background: rgba(240,240,240,1)
  li
    padding: 20px
// responsive
// @media (max-width: 812px)
</style>
