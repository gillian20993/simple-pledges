<template>
  <div id="app" class="et_monarch">
    
    <NaturalPledge />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import NaturalPledge from './components/NaturalPledge.vue'

export default {
  name: 'app',
  components: {
    NaturalPledge
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
@import url(https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css);
</style>
