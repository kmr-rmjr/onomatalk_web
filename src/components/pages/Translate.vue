<template>
  <v-container fluid>
    <p>{{part}}</p>
    <v-row justify="center">
      <v-col cols="12" lg="4" md="5" sm="6">
        <v-text-field
          outlined
          label="どこが痛みますか？"
          :value="part"
          @change="part = $event"
        ></v-text-field>
      </v-col>
      <v-col cols="12" lg="4" md="5" sm="6">
        <v-select
          outlined
          label="翻訳先"
        ></v-select>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" lg="4" md="10" sm="11">
        <toggle-bottuns
          justify="space-between"
          :option="{fab: true}"
          :active="activeColumn"
          :activeColor="'#FFBFBF'"
          :passiveColor="'#dddddd'"
          :lists="onomatopeLists"
          label="label"
          @my-click="activeColumn = $event"
        ></toggle-bottuns>

        <toggle-bottuns
          :className="['mx-2', 'mt-3']"
          :option="{rounded: true}"
          :active="selectedWord"
          :activeColor="'#FFBFBF'"
          :passiveColor="'#dddddd'"
          :lists="activeColumn.words"
          label="word"
          @my-click="selectedWord = $event"
        ></toggle-bottuns>
      </v-col>
      <v-col cols="12" lg="4" md="10">
        <v-card
          height="200"
          color="#FFBFBF"
        >
          <v-card-text>
            <p>{{translatedText}}</p>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ToggleBottuns from '../molecules/ToggleBottuns.vue';

export default {
  components: {
    ToggleBottuns,
  },
  data() {
    return {
      part: "",
      activeColumn: "",
      selectedWord: "",
      translatedText: "",
      languages: [{lang: '英語', code: 'en'}, {lang: 'フランス語', code: 'fr'}],
      onomatopeLists: {
        aColumn: {
          label: 'あ',
          words: [{word: 'イガイガ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}]
        },
        kColumn: {
          label: 'か',
          words: [{word: 'イガイガ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}]
        },
        sColumn: {
          label: 'さ',
          words: [{word: 'イガイガ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}]
        },
        tColumn: {
          label: 'た',
          words: [{word: 'イガイガ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}]
        },
        hColumn: {
          label: 'は',
          words: [{word: 'イガイガ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}]
        },
        mColumn: {
          label: 'ま',
          words: [{word: 'イガイガ', explanation: '説明文'}, {word: 'ウズウズ', explanation: '説明文'}]
        },
      }
    }
  },
  created() {
    this.activeColumn = this.onomatopeLists.aColumn;
    this.translatedText = 'こちらに翻訳結果が表示されます。'
  }
}
</script>

<style>
  body {
    font-family: Hiragino Sans,Meiryo,sans-serif;;
  }
</style>