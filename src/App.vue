<template>
  <div id="app">
    
    <Talents />
  </div>
</template>

<script>
import Talents from './components/Talents.vue'

export default {
  name: 'app',
  components: {
   Talents
  }
}
</script>

<style >
body{
  background-color: #eeeeee;
}
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; }*/

</style>
