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
  props: {
    lists: {
      type: [Array, Object],
      required: true
    },
    activeColor: {
      type: String,
      required: true
    },
    passiveColor: {
      type: String,
      required: true
    },
    active: {
      type: Object,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    option: {
      type: Object,
      required: false
    },
    justify: {
      type: String,
      required: false
    },
    className: {
      type: Array,
      required: false
    }

  },
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