<template>
  <chart-vue />
</template>

<script>
import chartVue from './components/chartVue.vue'
export default {
  name: 'App',
  components: {
    chartVue,
  },
  data() {
    return {}
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  height: 100vh !important;
}
</style>
