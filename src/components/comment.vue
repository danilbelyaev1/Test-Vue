<template>
  <div class="comment">
    <h4>{{comment.name}} // {{comment.email}}</h4>
    <p>{{comment.body}}</p>
  </div>
</template>

<script>
export default {
  name: "comment",
  props: {
    comment: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style lang="scss" scoped>
  .comment{
    border: 2px solid black;
    margin-top: 5px;
    padding: 10px;
  }
</style>