<template>
  <v-app>
    <v-app-bar absolute dark>
      <v-container light>
        <v-row
          style="max-width: 100%"
          justify="space-between"
          class="align-center"
        >
          <h1 class="float-left">Wheather App</h1>
          <v-text-field
            label="Search"
            placeholder="Search city..."
            solo
            light
            class="float-right align-center"
            style="max-width: 400px"
          ></v-text-field></v-row
      ></v-container>
    </v-app-bar>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      api_key: "0a779abe3a448790cdbd45cfee943301",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
};
</script>

<style scoped>
#app {
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#app.warm {
  background-image: url("./assets/warm-bg.webp");
}
main {
  height: 100vh;
  padding: 15%;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}
</style>
