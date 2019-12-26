<script>
// import { mapState, mapMutations } from "vuex";

import NavigationBar from "@/components/NavigationBar";
import AttributeSettings from "@/components/AttributeSettings";

export default {
  name: "Settings",
  components: { NavigationBar, AttributeSettings },
  inject: ["girderRest"],
  data() {
    let lightTheme = true;
    try {
      lightTheme = JSON.parse(localStorage.getItem("viameweb-light-theme"));
    } catch (ex) {} // eslint-disable-line
    this.$vuetify.theme.dark = !lightTheme;
    return { lightTheme };
  },
  watch: {
    lightTheme(value) {
      this.$vuetify.theme.dark = !value;
      try {
        localStorage.setItem("viameweb-light-theme", value);
      } catch (ex) {} // eslint-disable-line
    }
  }
};
</script>

<template>
  <v-content>
    <NavigationBar />
    <v-container>
      <v-card class="color-setting">
        <v-card-title class="pb-0">
          Colors
        </v-card-title>
        <v-card-text>
          <v-switch v-model="lightTheme" label="Light theme"></v-switch>
        </v-card-text>
      </v-card>
      <AttributeSettings class="mt-4" />
    </v-container>
  </v-content>
</template>
