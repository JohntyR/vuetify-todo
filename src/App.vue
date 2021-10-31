<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app :mobile-breakpoint="768">
      <v-img
        height="170"
        src="https://picsum.photos/id/11/500/300"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        class="pa-4 pt-7"
      >
        <v-avatar size="70" class="mb-2">
          <img src="https://cdn.vuetifyjs.com/images/john.jpg" alt="John" />
        </v-avatar>
        <div class="text-subtitle-1 font-weight-bold">John</div>
        <div class="text-subtitle-2">John@gmail</div>
      </v-img>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      src="https://picsum.photos/1920/1080?random"
      height="170"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <v-container class="pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-app-bar-title class="ml-4 text-h4">{{ $store.state.appTitle }}</v-app-bar-title>
        </v-row>
        <v-row>
          <live-date-time></live-date-time>
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: "Todo", icon: "mdi-format-list-checks", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
  }),
  components: {
    snackbar: require("@/components/Shared/Snackbar.vue").default,
    search: require("@/components/Tools/Search.vue").default,
    "live-date-time": require("@/components/Tools/LiveDateTime.vue").default,
  },
  mounted() {
    this.$store.dispatch('getTasks');
  },
};
</script>

<style lang="sass">
.v-app-bar-title__content
  width: 200px !important
</style>
