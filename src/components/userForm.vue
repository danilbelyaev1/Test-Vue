<template>
  <form @submit.prevent class="user-form">
    <vue-select
        @selectOption="selectSort"
        :options="sortOptions"
    />
    <vue-input
        placeholder="Поиск по номеру..."
        @changeValue="changeQuery"/>
  </form>
</template>

<script>
export default {
  name: "user-form",
  props: {
    sortOptions: {
      type: Array
    }
  },
  methods: {
    selectSort(value)  {
      this.$emit('update:selectedSort', value)
    },
    changeQuery(value)  {
      this.$emit('update:searchQuery', value)
    }
  }
}
</script>

<style lang="scss" scoped>
  .user-form{
    padding: 20px 0;
    display: flex;
    justify-content: space-between;
  }
</style>