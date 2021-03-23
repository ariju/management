<template>
  <v-parallax
    height="700"
    dark
    :src="require('@/assets/images/fitness-1882721_1920.jpg')"
  >
    <v-row
      align="center"
      justify="center"
    >
      <v-col
        class="text-center"
        cols="12"
      >
        <h1 class="display-1 font-weight-thin mb-4">
          トレーニングお疲れ様でした
        </h1>
        <h2 class="subheading">
          今日の成果を記録しよう!
        </h2>
      </v-col>
    </v-row>
  </v-parallax>
</template>

<script>
export default {
  middleware: ['checkAuth'],
  layout: "main",
}
</script>


