<template>
  <div id="app">
    <img src="./assets/logo.png">
    <div class="three fields">
      <cascade :config="config" v-model="choice" @change="change"></cascade>
    </div>
    <!-- <input :value="Object.keys(choice).join(',')"/>
    <input :value="Object.keys(choice).length>0?choice[Object.keys(choice)[0]]:'abc'"/> -->
    <div v-for="(value, key) in choice">
      {{ key }} : {{ value }}
    </div>
    <div>
    </div>
  </div>
</template>

<script>
import Cascade from 'src/index'
export default {
  name: 'app',
  data () {
      return {
          config: {
              "url":"/api/cascade",
          },
          choice: {}
      }
  },
  components: {
    cascade: Cascade
  },
  methods: {
      change:function(key, val) {
          console.log(key, val);
      },
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
