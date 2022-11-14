<template>
  <div id="app">
    <h1>HelloWorld Welcome To Weather App</h1>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "0a779abe3a448790cdbd45cfee943301",
    };
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
