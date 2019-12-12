<template>
  <div id="app">
    <Romaji2Kana />
  </div>
</template>

<script>
import Romaji2Kana from "./components/Romaji2Kana.vue";

export default {
  name: "app",
  components: {
    Romaji2Kana
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
