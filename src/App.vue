<template>
  <div id="app">
    <Request />
    <Response />
    
  </div>
</template>

<script>
import Request from './components/Request.vue'
import Response from './components/Response.vue'

export default {
  name: 'App',
  components: {
    Request,
    Response
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
