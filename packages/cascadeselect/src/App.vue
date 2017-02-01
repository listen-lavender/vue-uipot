<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div class="three fields">
      <cascade :config="config"></cascade>
    </div>
  </div>
</template>

<script>
import Cascade from './components/Cascade'
export default {
  name: 'app',
  data () {
      return {
          config: {
              "url":"/api/cascade",
          }
      }
  },
  components: {
    cascade: Cascade
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
