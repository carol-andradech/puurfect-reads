<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <ReadPage />
    <!-- Adicione esta linha para utilizar o componente ReadPage -->
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import ReadPage from "./components/ReadPage.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    ReadPage,
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
