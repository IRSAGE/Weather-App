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
            v-model="query"
            @keypress="getWeather"
          ></v-text-field></v-row
      ></v-container>
    </v-app-bar>
    <v-main
      id="app"
      :class="
        typeof weather.main != 'undefined' && weather.main.temp > 16
          ? 'warm'
          : ''
      "
    >
      <main>
        <WeatherComponent :weather="weather" />

        <div v-if="this.notFound == true" class="notfound">
          <h2 class="notfound-text">No Weather Found!</h2>
        </div>
      </main>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
import WeatherComponent from "./components/WeatherComponent.vue";
export default {
  name: "App",
  components: {
    WeatherComponent,
  },
  data() {
    return {
      api_key: "0a779abe3a448790cdbd45cfee943301",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
      notFound: false,
    };
  },
  methods: {
    getWeather(e) {
      if (e.key == "Enter") {
        axios
          .get(
            `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
          )
          .then((res) => {
            this.notFound = false;
            this.weather = res.data;
          })
          .catch(() => {
            this.weather = {};
            this.notFound = true;
          });
      }
    },
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

.notfound {
  display: flex;
  justify-content: center;
  align-items: center;
}
.notfound-text {
  color: #fff;
  font-size: 50px;
  font-weight: 700;
  font-style: italic;
}
</style>
