<template>
  <input type="text" @input="changeValue"/>
</template>

<script>
export default {
  name: "vue-input",
  props: {
    options: {
      type: Array,
      default: () => []
    }
  },
  methods:{
    changeValue(e) {
      this.$emit('changeValue', e.target.value)
    }
  },
}
</script>

<style scoped>
  input{
    min-width: calc(50% - 20px);
    border: 2px solid black;
    padding: 10px;
  }
</style>