<template>
  <div id="app">
    <div class="maindiv">
      <container />
    </div>
  </div>
</template>

<script>
import container from "./components/container";

export default {
  name: "App",
  components: {
    container
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.maindiv {
  width: 100vw;
  height: 100vh;
  background-color: rgb(255, 255, 255);
}
</style>
