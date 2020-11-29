<template>
  <v-app>
    <header>
      <v-app-bar
        flat
        color="#FFBFBF"
      ></v-app-bar>
    </header>
    <v-main>
      <translate></translate>
    </v-main>
    <v-footer>
      <p>footer</p>
    </v-footer>
  </v-app>
</template>

<script>
import Translate from '@/components/pages/Translate.vue';

export default {
  components: {
    Translate,
  }
}
</script>

<style scoped>
  body {
    font-family: Hiragino Sans,Meiryo,sans-serif;;
  }
</style>