<template>
  <div class="comment-form">
    <vue-input v-model="comment.name" placeholder="Your name"/>
    <vue-input v-model="comment.email" placeholder="Your email"/>
    <vue-input v-model="comment.body" placeholder="Your comment"/>
    <vue-btn>Send</vue-btn>
  </div>
</template>

<script>
export default {
  name: "commentForm",
  components: {},

  data(){
    return{
      comment:{
        name: '',
        email: '',
        body: '',
      }
    }
  },
  props:{
    comments:{
      type: Array,
    },
  },
}
</script>

<style lang="scss" scoped>
  input{
    width: 100%;
    margin-top: 10px;
  }
  .btn{
    margin-bottom: 20px;
  }
</style>