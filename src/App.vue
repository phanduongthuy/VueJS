<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
<!--    <HelloWorld />-->

    <hw01/>
    
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

import hw01 from "./components/exercises/unit01/hw01";

export default {
  name: 'App',
  components: {
    hw01,
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
