<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <YOLOAnnotation />
  </div>
</template>

<script>
import YOLOAnnotation from "./components/YOLOAnnotattion";

export default {
  name: "app",
  components: {
    YOLOAnnotation
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
  margin-top: 60px;
}
</style>
