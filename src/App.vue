<template>
  <v-app>
    <v-app-bar absolute dark>
      <v-container light>
        <div class="d-flex justify-space-between align-center">
          <div class="d-flex justify-space-between align-center">
            <v-avatar class="profile" size="64" tile>
              <v-img
                src="https://www.freeiconspng.com/thumbs/weather-icon-png/weather-icon-png-2.png"
              ></v-img>
            </v-avatar>
            <h1 class="float-left">Weather App</h1>
          </div>

          <v-text-field
            label="Search"
            placeholder="Search city..."
            solo
            single-line
            light
            style="max-width: 400px"
            v-model="query"
            @keypress="getWeather"
            class="input"
          ></v-text-field>
        </div>
      </v-container>
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
        <div
          v-if="this.loading"
          class="d-flex justify-center align-center flex-column white--text"
        >
          <v-avatar class="profile" size="164" tile>
            <v-img
              src="https://harbourmaster.org/sites/default/files/2021-09/Sunrise_1.gif"
            ></v-img>
          </v-avatar>
          <h2 class="font-weight-bold text-h4">Loading!</h2>
        </div>
        <div
          v-if="this.notFound"
          class="d-flex justify-center align-center flex-column white--text"
        >
          <v-avatar class="profile" size="164" tile>
            <v-img
              src="https://www.freeiconspng.com/thumbs/weather-icon-png/weather-icon-png-2.png"
            >
            </v-img>
          </v-avatar>
          <h2 class="font-weight-bold text-h3">No Weather Found!</h2>
        </div>
        <div
          v-if="
            !this.notFound &
            (typeof weather.main == 'undefined') &
            !this.loading
          "
          class="d-flex justify-center align-center flex-column white--text"
        >
          <v-avatar class="profile" size="164" tile>
            <v-img
              src="https://www.freeiconspng.com/thumbs/weather-icon-png/weather-icon-png-2.png"
            ></v-img>
          </v-avatar>
          <h2 class="font-weight-bold text-h2">Welcome To Weather App</h2>
          <p class="text-h6 mx-4 align-center">
            You can search weather condition in any area by typing the name of
            the city or country you want.
          </p>
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
      loading: false,
    };
  },
  methods: {
    getWeather(e) {
      if (e.key == "Enter") {
        this.weather = {};
        this.notFound = false;
        this.loading = true;
        axios
          .get(
            `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
          )
          .then((res) => {
            this.loading = false;
            this.notFound = false;
            this.weather = res.data;
          })
          .catch(() => {
            this.loading = false;
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
.input {
  margin-top: 32px !important;
}
</style>
