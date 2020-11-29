<template>
  <v-container fluid>
    <v-row justify="center">
      <v-col cols="12" lg="4" md="5" sm="6">
        <v-text-field
          :color="activeColor"
          outlined
          label="どこが痛みますか？"
          :value="part"
          @change="part = $event"
        ></v-text-field>
      </v-col>
      <v-col cols="12" lg="4" md="5" sm="6">
        <v-select
          :color="activeColor"
          v-model="targetLang"
          :items="languages"
          item-text="lang"
          item-value="code"
          label="翻訳先"
          outlined
        ></v-select>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" lg="4" md="10" sm="11">
        <toggle-bottuns
          justify="space-between"
          :option="{fab: true}"
          :active="activeColumn"
          :activeColor="activeColor"
          :passiveColor="passiveColor"
          :lists="onomatopeLists"
          label="label"
          @my-click="activeColumn = $event"
        ></toggle-bottuns>

        <toggle-bottuns
          :className="['mx-2', 'mt-3']"
          :option="{rounded: true}"
          :active="selectedWord"
          :activeColor="activeColor"
          :passiveColor="passiveColor"
          :lists="activeColumn.words"
          label="word"
          @my-click="selectedWord = $event"
        ></toggle-bottuns>
      </v-col>
      <v-col cols="12" lg="4" md="10">
        <v-card
          height="150"
          :color="activeColor"
          id="translated-area"
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
import ToggleBottuns from '@/components/molecules/ToggleBottuns.vue';
import Axios from 'axios';
import languageList from '@/assets/language_list.json'

export default {
  props: {
    activeColor: {
      type: String,
      required: true,
    },
    passiveColor: {
      type: String,
      required: true,
    }
  },
  components: {
    ToggleBottuns,
  },
  data() {
    return {
      part: "",
      activeColumn: {lebel: "", words: []},
      selectedWord: {word: "", explanation: ""},
      translatedText: "",
      targetLang: "en",
      languages: languageList,
      onomatopeLists: [{label: "", words: []}],
    }
  },
  methods: {
    translate() {
      if(this.part != "" && this.selectedWord.word != "" && this.targetLang != "") {
        this.$vuetify.goTo('#translated-area');
        this.translatedText = "翻訳中...";
        Axios.post(process.env.VUE_APP_TRANSLATE_URL, {
          source: 'ja',
          target: this.targetLang,
          transcript: this.part + this.selectedWord.explanation
        }).then(data => {
          this.translatedText = data.data.translatedText;
        })
      }
    }
  },
  watch: {
    part() {
      this.translate();
    },
    selectedWord() {
      this.translate();
    },
    targetLang() {
      this.translate();
    }
  },
  created() {
    Axios.get(process.env.VUE_APP_GET_ONOMATOPE_LIST_URL)
        .then(responce => {
          this.onomatopeLists = responce.data;
          this.activeColumn = this.onomatopeLists[0];
        });
    this.translatedText = 'こちらに翻訳結果が表示されます。'
  }
}
</script>