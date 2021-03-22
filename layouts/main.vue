<template>
  <v-app>
    <v-navigation-drawer app v-model="drawer" clipped>
      <v-container>
        <v-list dense nav>
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="title grey--text text--darken-2">
                Navigation lists
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
        <v-divider></v-divider>
        <v-list-item>
          <v-btn text nuxt-link to="/" class="m-5"
            ><v-icon>mdi-home</v-icon>HOME</v-btn
          >
        </v-list-item>
        <v-list-item>
          <v-btn text nuxt-link to="/bmi" class="m-5"
            ><v-icon>mdi-calculator</v-icon>bmi指数</v-btn
          >
        </v-list-item>
        <v-list-item>
          <v-btn text nuxt-link to="/calendar" class="m-5"
            ><v-icon>mdi-calendar</v-icon>カレンダー</v-btn
          >
        </v-list-item>
        <v-list-item>
          <v-btn text nuxt-link to="/pomodoro" class="m-5"
            ><v-icon>mdi-timer</v-icon>カウントダウンタイマー</v-btn
          >
        </v-list-item>
      </v-container>
    </v-navigation-drawer>
    <v-app-bar color="primary" dark app clipped-left>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Workout</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-menu offset-y>
          <template v-slot:activator="{ on }">
            <v-btn v-on="on" text>Support<v-icon>mdi-menu-down</v-icon></v-btn>
          </template>
          <v-list dense nav>
            <v-subheader>Get help</v-subheader>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-icon>
                  <v-btn text @click="logout"
                    ><v-icon>mdi-logout</v-icon>ログアウト</v-btn
                  >
                </v-list-item-icon>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-toolbar-items>
    </v-app-bar>
    <v-main>
    <nuxt />
    </v-main>
    <v-footer color="primary" dark app>
      Workout
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null
    };
  },
  methods: {
    logout() {
      this.$fireAuth
        .signOut()
        .then(() => {
          console.log("ログアウト");
          this.$router.push("/login");
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>
