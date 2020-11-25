/* 
  複数のボタンから1つだけが選択されるコンポーネント。
 */

<template>
  <div>
    <v-btn
      v-bind="option"
      dark
      :color="ColoringBtn(list, activeColor, passiveColor)"
      v-for="list in lists"
      :key='list.label'
      @click="ChangeActive(list)"
    >{{list[label]}}</v-btn>
  </div>
</template>

<script>
export default {
  props: ['lists', 'activeColor', 'passiveColor', 'active', 'label', 'option'],
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