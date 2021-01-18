<template>
  <div id="app">
    <SliderTest/>
  </div>
</template>

<script>
import SliderTest from './components/SliderTest.vue'

export default {
  name: 'App',
  components: {
    SliderTest
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
