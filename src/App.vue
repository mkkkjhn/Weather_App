<template>
  <weather-app></weather-app>
</template>

<script>
import WeatherApp from '@/components/WeatherApp'

export default {
  name: 'App',
  components: {
    WeatherApp
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
