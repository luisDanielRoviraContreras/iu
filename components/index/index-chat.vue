<template>
  <div
    :style="{
      transform: `translate(${move}px)`
    }"
    class="index-chat">
    <input @focus="$router.push('/search/')" type="text">
    <div class="con-chats">
      <div v-for="item in 50" :key="item" @click="$router.push('/chat/')" class="chat-item">
        Chat {{ move }}
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
@Component
export default class indexChat extends Vue {
  get move() {
    return (this.$parent as any).move
  }
}
</script>
<style lang="sass" scoped>
.index-chat
  min-width: 100%
  flex: 1
  scroll-snap-align: center
  overflow: auto
  height: 100%
  position: relative
  z-index: 200
  background: #fff
  .con-chats
    .chat-item
      padding: 20px
// responsive
// @media (max-width: 812px)
</style>
