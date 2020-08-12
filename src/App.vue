<template>
  <div id="app">
    <TurnMove />
  </div>
</template>

<script>
import TurnMove from './components/TurnMove.vue'

export default {
  name: 'App',
  components: {
    TurnMove,
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
