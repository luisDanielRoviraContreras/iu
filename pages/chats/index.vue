<template>
  <div class="chats page">
    index
    <button @click="$router.push('search')">
      Search
    </button>
    <ul>
      <li @click="$router.push('/chats/chat')" v-for="item in 20" :key="item">
        Esto es un chat <b>{{item}}</b>
      </li>
    </ul>
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
export default class chats extends Vue {}
</script>
<style lang="sass" scoped>
.chats
  background: rgba(240,240,200,1)
  overflow: auto
  li
    padding: 20px
// responsive
// @media (max-width: 812px)
</style>
