<template>
  <div id="app">
    <ToDo />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import Vuetify from '@/components/Vuetify.vue';
import ToDo from '@/components/ToDo.vue';

export default {
  name: 'App',
  components: {
    // Vuetify,
    ToDo,
  },
};
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
