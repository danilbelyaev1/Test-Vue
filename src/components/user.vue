<template>
  <li class="user-card" :class="{opened : posts.length >= 1}">
    <div class="id">
      {{user.id}}.
    </div>
    <div class="user-data">
      <strong>Username: </strong>
      {{user.username}}
    </div>
    <div class="user-data">
      <strong>Name:</strong>
      {{user.name}}
    </div>
    <div class="user-data">
      <strong>City:</strong>
      {{user.address.city}}
    </div>
    <div class="user-data">
      <strong>
        Phone:
      </strong>
      {{user.phone}}
    </div>
    <vue-btn v-if="posts.length < 1" @click="fetchPosts">Posts</vue-btn>
    <post-wrap
      :posts="posts"
    />
  </li>
</template>

<script>
import postWrap from "@/components/postWrap";
export default {
  name: "user",
  components: {postWrap},
  data() {
    return {
      posts: [],
    }
  },
  props: {
    user: {
      type: Object,
      required: true,
    },
  },
  methods: {
    async fetchPosts () {
      try{
        this.isLoading = true;
        fetch(`https://jsonplaceholder.typicode.com/users/${this.user.id}/posts`)
            .then(response => response.json())
            .then(json => {
              this.posts = json
            })
      }
      catch (e) {
        alert('Error')
      } finally {
        this.isLoading = false;
      }
    },
  },
}
</script>

<style lang="scss" scoped>
  li{
    list-style: none;
    border: 2px solid black;
    margin-bottom: 20px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    width: fit-content;
    min-width: 49%;
    justify-content: space-between;
    .id{
      border: 2px solid black;
      padding: 5px 10px;
      display: flex;
      width: fit-content;
      margin-bottom: 5px;
    }
    .user-data{
      margin-bottom: 4px;
    }
    &.opened{
      min-width: 100%;
    }
  }
</style>