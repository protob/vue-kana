<template>
  <div id="app">
    <VueKana />
  </div>
</template>

<script>
import VueKana from "./components/VueKana.vue";

export default {
  name: "app",
  components: {
   VueKana
  }
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
