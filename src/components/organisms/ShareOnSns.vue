<template>
  <div class="d-flex justify-center">
    <v-col cols="11" lg="4" md="6" sm="9" class="text-center">
      <p class="title font-weight-medium grey--text text--darken-3 mt-16">SNSでシェアする</p>
      <v-card height="200" class="d-flex justify-space-between flex-wrap align-center px-10 mb-16">
        <v-btn
          fab
          icon
          target="_blank"
          v-for="site in sns"
          :key="site.url"
          :href="site.url"
        >
          <fa-icon size="2x" :icon="site.icon"/>
        </v-btn>

        <v-btn
          fab
          icon
          :href="shareOnHatena"
          target="_blank"
        >
          <span class=" headline font-weight-bold">B!</span>
        </v-btn>
      </v-card>
    </v-col>
  </div>
</template>

<script>
export default {
  data() {
    return {
      url: process.env.VUE_APP_URL,
      textTwitter: "オノマトークを使ってオノマトペを翻訳しよう！",
      hashtag: "オノマトーク",
    }
  },
  computed: {
    sns() {
      return [
        {
          icon: ['fab', 'twitter'],
          url: `https://twitter.com/intent/tweet?url=${this.url}&text=${this.textTwitter}&hashtags=${this.hashtag}`
          },
        {
          icon: ['fab', 'facebook'],
          url: `https://www.facebook.com/sharer/sharer.php?u=${this.url}`
          },
        {
          icon: ['fab', 'line'],
          url: `http://line.me/R/msg/text/?${this.text} ${this.url}"`
          },
      ]
    },
    shareOnHatena() {
      return `http://b.hatena.ne.jp/entry/${this.url}`
    }
  }
}
</script>

<style>

</style>