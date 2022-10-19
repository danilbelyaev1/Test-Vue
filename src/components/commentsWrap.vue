<template>
  <div class="comments-wrap">
    <comment-form
      :comments="comments"
      @create="createComment"
    />
    <comment
      v-for="comment in comments"
      :comment="comment"
    />
  </div>
</template>

<script>
import comment from "@/components/comment";
import CommentForm from "@/components/commentForm";
export default {
  name: "commentsWrap",
  components: {
    CommentForm,
    comment,
  },
  props: {
    comments: {
      type: Array,
      required: true,
    }
  },
}
</script>

<style scoped>
</style>