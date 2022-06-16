<template>
  <h1 class="container bg-primary fixed-top pt-2 pb-2">You feed</h1>
  <Youfeed />
</template>

<script>
import Youfeed from './components/Youfeed.vue'

export default {
  name: 'App',
  components: {
    Youfeed
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
