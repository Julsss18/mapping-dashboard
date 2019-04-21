<template>
  <div id="app">
    <MapDashboard/>
  </div>
</template>

<script>
import MapDashboard from './components/MapDashboard';

export default {
  name: 'app',
  components: {
    MapDashboard
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
