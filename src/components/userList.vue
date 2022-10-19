<template>
  <ul class="user-list">
    <user
        v-for="user in users"
        :key="user.id"
        :user="user"

    />
  </ul>
</template>

<script>
import user from "@/components/user";
export default {
  components: {
    user,
  },
  props: {
    users: {
      type: Array,
      required: true,
    },
  },
  name: "userList",
}
</script>

<style lang="scss" scoped>
  ul{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    width: 100%;
    justify-content: space-between;
  }
</style>