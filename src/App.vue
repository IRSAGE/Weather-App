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
        <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
          <div class="location-box">
            <div class="location">
              {{ weather.name }}, {{ weather.sys.country }}
            </div>
            <div class="date">{{ dateBuilder() }}</div>
          </div>

          <div class="weather-box">
            <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
            <div class="weather">{{ weather.weather[0].main }}</div>
          </div>
        </div>
        <div v-if="this.notFound == true" class="notfound">
          <h2 class="notfound-text">No Weather Found!</h2>
        </div>
      </main>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  name: "App",

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
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
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
.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-wrap {
  align-self: center;
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
