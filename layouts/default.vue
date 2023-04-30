<template>
  <v-app dark>
    <v-navigation-drawer v-model="drawer" :rail="mini_variant" :rail-width="100" fixed app>
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i" :to="item.to" router exact>
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item class="pa-0">
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="mini_variant = !mini_variant">
        <v-icon>mdi-{{ `chevron-${mini_variant ? "right" : "left"}` }}</v-icon>
      </v-btn>
      <v-toolbar-title>{{ title }}</v-toolbar-title>
      <v-spacer />
      <v-btn icon rounded circle>
        <v-icon>mdi-account</v-icon>
      </v-btn>
      <v-btn icon rounded>
        <v-icon>mdi-cart-outline</v-icon>
      </v-btn>
      <v-btn icon rounded @click="toggleTheme">
        <v-icon>mdi-theme-light-dark</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <slot />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import { useTheme } from "vuetify";

export default {
  name: "default",
  data() {
    return {
      drawer: true,
      mini_variant: true,
      items: [
        {
          icon: "mdi-apps",
          title: "Welcome",
          to: "/",
        },
        {
          icon: "mdi-chart-bubble",
          title: "Sign Up",
          to: "/signup",
        },
        {
          icon: "mdi-chart-bubble",
          title: "Reset",
          to: "/reset-password",
        },
      ],
      title: "E-COM",
    };
  },
  setup() {
    const theme = useTheme();

    return {
      theme,
      toggleTheme: () =>
        (theme.global.name.value = theme.global.current.value.dark ? "light" : "dark"),
    };
  },
};
</script>
