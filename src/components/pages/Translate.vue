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
        <p class="subtitle-1 headline grey--text text--darken-3">どのように痛みますか？</p>
        <toggle-bottuns
        v-model="activeColumn"
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
          :className="['mx-2', 'mt-4','mb-6']"
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
        <p id="translated-area" class="subtitle-1 headline grey--text text--darken-3">翻訳結果</p>
        <v-card
          height="150"
          :color="activeColor"
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
      translatedText: "こちらに翻訳結果が表示されます。",
      targetLang: "en",
      languages: languageList,
      onomatopeLists: {
        Acolumn: {
          label: 'あ',
          words: []
        },
        Kcolumn: {
          label: 'か',
          words: []
        },
        Scolumn: {
          label: 'さ',
          words: []
        },
        Tcolumn: {
          label: 'た',
          words: []
        },
        Hcolumn: {
          label: 'は',
          words: []
        },
        Mcolumn: {
          label: 'ま',
          words: []
        },
      },
    }
  },
  methods: {
    translate() {
      if(this.part != "" && this.selectedWord.word != "" && this.targetLang != "") {
        this.$vuetify.goTo('#translated-area');
        this.translatedText = "翻訳中...";
        Axios.get(process.env.VUE_APP_API_URL + 'translate/', {
          params: {
            target: this.targetLang,
            text: this.part + this.selectedWord.explanation
          }
        }).then(data => {
          this.translatedText = data.data.translated_text;
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
    this.activeColumn = this.onomatopeLists.Acolumn;
    Axios.get(process.env.VUE_APP_API_URL + 'acolumn/')
        .then(responce => {
          this.onomatopeLists.Acolumn.words = responce.data;
        });
    Axios.get(process.env.VUE_APP_API_URL + 'kcolumn/')
        .then(responce => {
          this.onomatopeLists.Kcolumn.words = responce.data;
        });
    Axios.get(process.env.VUE_APP_API_URL + 'scolumn/')
        .then(responce => {
          this.onomatopeLists.Scolumn.words = responce.data;
        });
    Axios.get(process.env.VUE_APP_API_URL + 'tcolumn/')
        .then(responce => {
          this.onomatopeLists.Tcolumn.words = responce.data;
        });
    Axios.get(process.env.VUE_APP_API_URL + 'hcolumn/')
        .then(responce => {
          this.onomatopeLists.Hcolumn.words = responce.data;
        });
    Axios.get(process.env.VUE_APP_API_URL + 'mcolumn/')
        .then(responce => {
          this.onomatopeLists.Mcolumn.words = responce.data;
        });
  }
}
</script>