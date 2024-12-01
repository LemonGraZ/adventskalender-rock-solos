<template>
  <v-banner color="#C4B180" icon="mdi-calendar-today" lines="one">
    <v-banner-text> Nicht Heute!</v-banner-text>

    <template v-slot:actions>
      <v-btn color="#C4B180" @click="goToToday"> Gehe zu Heute </v-btn>
    </template>
  </v-banner>
</template>

<script>
export default {
  methods: {
    goToToday() {
      const newUrl = `${window.location.origin}/${
        window.location.pathname.split("/")[1]
      }/`;
      window.location.replace(newUrl);
    },
  },
};
</script>
