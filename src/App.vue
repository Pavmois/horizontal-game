<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Roulette msg="Испытай свою удачу в беспроигрышной рулетке"/>
  </div>
</template>

<script>
import Roulette from './components/Roulette.vue'

export default {
  name: 'App',
  components: {
    Roulette
  }
}
</script>

<style>
body {
  background-color: #2c3e50;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: aliceblue;
  margin-top: 60px;
}
</style>
