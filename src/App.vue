<template>
  <div id="app">
    <app-music-player />
  </div>
</template>

<script>
import AppMusicPlayer from '@/components/MusicPlayer'

export default {
  name: 'App',
  components: {
    AppMusicPlayer
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
