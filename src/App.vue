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
    </v-main>
    <v-footer
      padless
      dark
    >
      <v-card :color="colors.accent" tile width="100%">
        <v-card-text class="headline white--text">OGATA PROJECT 2020</v-card-text>
        <v-card-text class="">
          <v-btn class="mx-4 text-left" icon>
            <fa-icon size="2x" :icon="['fab', 'twitter']"/>
          </v-btn>
          <v-btn class="mx-4" icon href="https://github.com/kmr-rmjr/onomatalk_web" target="_blank">
            <fa-icon size="2x" :icon="['fab', 'github']"/>
          </v-btn>
        </v-card-text>
        <v-divider />
        <v-card-text class="font-weight-medium white--text text-center">©OGATA PROJECT 2020</v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
import Translate from '@/components/pages/Translate.vue';

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
  }
}
</script>

<style>
  body {
    font-family: Hiragino Sans,Meiryo,sans-serif;
  }
</style>