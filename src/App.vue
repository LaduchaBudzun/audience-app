<template>
  <div id="app">
    
    <Audience/>
  </div>
</template>

<script>
import Audience from './components/Audience.vue'

export default {
  name: 'App',
  components: {
    Audience
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
