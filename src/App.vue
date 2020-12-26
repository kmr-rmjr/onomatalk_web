<template>
  <v-app>
    <header>
      <v-app-bar
        dark
        flat
        :color="colors.primary"
      >
        <v-toolbar-title>Onoma Talk</v-toolbar-title>
      </v-app-bar>
    </header>
    <v-main>
      <translate
        :activeColor="colors.primary"
        :passiveColor="colors.passive"
      ></translate>
      <share-on-sns></share-on-sns>
    </v-main>
    <v-footer
      padless
      dark
    >
      <v-card :color="colors.accent" tile width="100%">
        <v-card-text class="title white--text">OGATA PROJECT 2020</v-card-text>
        <v-divider />
        <v-card-text class="font-weight-medium white--text text-center">©OGATA PROJECT 2020, SENSHU University</v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
import Translate from '@/components/pages/Translate.vue';
import ShareOnSns from './components/organisms/ShareOnSns.vue';

export default {
  data() {
    return {
      colors: {
        primary: '#FFBFBF',
        passive: '#BDBDBD',
        accent: '#444444',
      }
    }
  },
  components: {
    Translate,
    ShareOnSns,
  }
}
</script>


    ShareOnSns<style>
  body {
    font-family: Hiragino Sans,Meiryo,sans-serif;
  }
</style>