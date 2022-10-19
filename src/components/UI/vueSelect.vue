<template>
  <select @change="selectOption">
    <option disabled value="one">Выберите параметр фильтрации</option>
    <option v-for="option in options" :key="option.value" :value="option.value" >
      {{option.name}}
    </option>
  </select>
</template>

<script>
export default {
  name: "vue-select",
  props: {
    options: {
      type: Array,
      default: () => []
    }
  },
  methods:{
    selectOption(e) {
      this.$emit('selectOption', e.target.value)
    }
  },
}
</script>

<style scoped>
  select{
    min-width: calc(50% - 20px);
    border: 2px solid black;
    padding: 10px;
  }
</style>