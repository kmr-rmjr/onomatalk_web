/* 
  複数のボタンから1つだけが選択されるコンポーネント。
 */

<template>
  <v-row :justify="justify">
    <v-btn
      :class="className"
      v-bind="option"
      dark
      :color="ColoringBtn(list, activeColor, passiveColor)"
      v-for="list in lists"
      :key='list.label'
      @click="ChangeActive(list)"
    >{{list[label]}}</v-btn>
  </v-row>
</template>

<script>
export default {
  props: ['lists', 'activeColor', 'passiveColor', 'active', 'label', 'option', 'justify', 'className'],
  methods: {
    ChangeActive(lab) {
      this.$emit('my-click', lab);
    },
    ColoringBtn(lab, activeColor, passiveColor) {
      return lab == this.active ? activeColor : passiveColor
    }
  }
}
</script>

<style>

</style>