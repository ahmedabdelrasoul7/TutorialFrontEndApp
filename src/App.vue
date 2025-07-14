<template>
  <img alt="Vue logo" src="./assets/logo.png" width="100px" height="50px">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  mounted() {
    document.title = "My Custom Tab Title";
  },
  components: {
    HelloWorld
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
  margin-top: px;
}
</style>
