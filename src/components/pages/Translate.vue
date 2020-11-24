<template>
  <h1>Hello World.</h1>
</template>

<script>
export default {
  data() {
    return {
      part: "",
      activeColumn: null,
      selectedWord: null,
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

}
</script>

<style>
  body {
    font-family: Hiragino Sans,Meiryo,sans-serif;;
  }
</style>