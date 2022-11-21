<template>
  <div
    v-if="loading"
    class="d-flex justify-center align-center flex-column white--text"
  >
    <v-avatar class="profile" size="164" tile>
      <v-img
        src="https://harbourmaster.org/sites/default/files/2021-09/Sunrise_1.gif"
      ></v-img>
    </v-avatar>
    <h2 class="font-weight-bold text-h4">Loading!</h2>
  </div>
</template>

<script>
export default {
  name: "LoadingComponent",
  props: ["loading"],
};
</script>
