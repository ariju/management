<template>
  <v-app>
    <v-main class="content">
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <v-card class="elevation-12">
              <v-toolbar color="primary" dark flat>
                <v-toolbar-title>Login form </v-toolbar-title>
                <v-spacer />
              </v-toolbar>
              <v-card-title>
                <h1 class="display-1">ログイン</h1>
              </v-card-title>
              <v-card-text>
                <v-form class="w-full" @submit.prevent="onSubmit">
                  <v-btn type="submit" class="info">
                    Google でログイン
                  </v-btn>
                </v-form>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  middleware: ["checkLogin"],
  methods: {
    onSubmit() {
      const provider = new this.$firebase.auth.GoogleAuthProvider();
      this.$fireAuth.signInWithRedirect(provider);
    }
  }
};
</script>

<style scoped>
.content {
  height: 664px;
  display: flex;
  width: 100%;
  background-size: cover;
  background-image: url("~@/assets/images/machines-91849_1280.jpg");
}
</style>
