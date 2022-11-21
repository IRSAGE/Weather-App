<template>
  <div
    v-if="notFound"
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
</template>

<script>
export default {
  name: "NotFound",
  props: ["notFound"],
};
</script>
