<template>
  <div
    v-if="!notFound && typeof weather.main == 'undefined' && !loading"
    class="d-flex justify-center align-center flex-column white--text"
  >
    <v-avatar class="profile" size="164" tile>
      <v-img
        src="https://www.freeiconspng.com/thumbs/weather-icon-png/weather-icon-png-2.png"
      ></v-img>
    </v-avatar>
    <h2 class="font-weight-bold text-h2">Welcome To Weather App</h2>
    <p class="text-h5 mt-6 text-center">
      You can search weather condition in any area by typing the name of the
      city or country you want and hit Enter.
    </p>
  </div>
</template>

<script>
export default {
  name: "WelcomeComp",
  props: ["notFound", "loading", "weather"],
};
</script>
