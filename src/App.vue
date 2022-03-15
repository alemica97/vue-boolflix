<template>
  <div id="app">
    <myMain />
  </div>
</template>

<script>
import myMain from './components/Main.vue'

export default {
  name: 'App',
  components: {
    myMain,
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
