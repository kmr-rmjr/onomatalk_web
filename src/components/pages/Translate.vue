<template>
  <v-app>
    <v-container fluid>
      <v-row justify="center">
        <v-col cols="12" lg="4">
          <v-text-field
            outlined
            label="どこが痛みますか？"
          ></v-text-field>
        </v-col>
        <v-col cols="12" lg="4">
          <v-select
            outlined
            label="翻訳先"
          ></v-select>
        </v-col>
      </v-row>
      <v-row justify="center">
        <v-col cols="12" lg="4">
          <togle-bottuns
            :option="{fab: true}"
            :active="activeColumn"
            :activeColor="'#FFBFBF'"
            :passiveColor="'#dddddd'"
            :lists="onomatopeLists"
            label="label"
            @my-click="activeColumn = $event"
          ></togle-bottuns>

          <togle-bottuns
            :option="{rounded: true}"
            :active="selectedWord"
            :activeColor="'#FFBFBF'"
            :passiveColor="'#dddddd'"
            :lists="activeColumn.words"
            label="word"
            @my-click="selectedWord = $event"
          ></togle-bottuns>
        </v-col>
        <v-col cols="12" lg="4">
          <v-card
            height="200"
            color="#FFBFBF"
          >
            <v-card-text>
              <p>Test</p>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import TogleBottuns from '../molecules/TogleBottuns.vue';

export default {
  components: {
    TogleBottuns,
  },
  data() {
    return {
      part: "",
      activeColumn: "",
      selectedWord: "",
      languages: [{lang: '英語', code: 'en'}, {lang: 'フランス語', code: 'fr'}],
      onomatopeLists: {
        aColumn: {
          label: 'あ',
          words: [{word: 'イガイガ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}]
        },
        kColumn: {
          label: 'か',
          words: [{word: 'イガイガ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}]
        },
      }
    }
  },
  created() {
    this.activeColumn = this.onomatopeLists.aColumn;
  }
}
</script>

<style>
  body {
    font-family: Hiragino Sans,Meiryo,sans-serif;;
  }
</style>