<template>
  <div id="app">
    <LoginScreen></LoginScreen>
  </div>
</template>

<script>
  import LoginScreen from './components/LoginScreen.vue'
  
  export default {
    name: 'app',
    components: {
      LoginScreen
    },
  
    data() {
      return {}
    },
  
    methods: {
    }
  }
</script>

<style>
  #app {
    font-family: -apple-system, BlinkMacSystemFont, "San Francisco";
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    height: 100%;
  }
</style>
