<template>
  <div class="post-wrap" v-if="posts.length >= 1" >
    <vue-btn @click="posts.length = 0">Close posts</vue-btn>
    <post
      v-for="post in posts"
      :post="post"
    />
  </div>
</template>

<script>
import Post from "@/components/post";
export default {
  name: "postWrap",
  components: {Post},
  props: {
    posts: {
      type: Array,
    }
  }
}
</script>

<style lang="scss" scoped>
  .post-wrap{
    margin-top: 0px;
    position: relative;
    max-height: 600px;
    overflow-y: scroll;
    &::-webkit-scrollbar{
      opacity: 0;
      display: none;
    }
  }
  .close{
    cursor: pointer;
    position: absolute;
    right: 0;
    top: -39px;
    font-size: 25px;
  }
  button{
    margin-bottom: 30px;
  }
</style>