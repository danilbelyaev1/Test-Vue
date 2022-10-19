<template>
  <div class="post">
    <h3 class="post-title">
      {{post.title}}
    </h3>
    <p class="post-body">
      {{post.body}}
    </p>
    <div v-if="!comments.length" @click="fetchComments" class="post-comments-length">
      <svg version="1.0" xmlns="http://www.w3.org/2000/svg"
           width="30" height="30" viewBox="0 0 1280.000000 1280.000000"
           preserveAspectRatio="xMidYMid meet">
            <g transform="translate(0.000000,1280.000000) scale(0.100000,-0.100000)"
            fill="#000000" stroke="none">
            <path d="M6330 12030 c-869 -39 -1846 -263 -2595 -595 -360 -159 -751 -383
            -1033 -592 -41 -31 -144 -96 -226 -146 -639 -381 -1136 -814 -1506 -1312 -372
            -499 -552 -876 -684 -1436 -88 -372 -112 -587 -103 -904 7 -236 30 -401 93
            -675 81 -353 158 -577 290 -841 200 -400 500 -806 850 -1149 248 -243 475
            -424 812 -647 192 -128 292 -213 497 -424 179 -184 259 -291 343 -458 l67
            -135 3 -109 c4 -129 -4 -160 -88 -332 -110 -225 -233 -386 -525 -685 -224
            -229 -255 -274 -287 -410 l-24 -105 26 -105 c32 -132 80 -206 179 -274 69 -47
            88 -53 242 -86 112 -23 206 -17 440 30 1315 263 3342 1081 4952 1996 395 225
            650 383 1134 700 133 87 361 237 505 331 145 95 364 246 488 335 124 88 270
            193 325 231 508 357 846 673 1143 1070 379 506 553 864 687 1412 99 402 120
            584 112 937 -6 270 -23 396 -92 695 -130 561 -280 895 -616 1369 -356 501
            -748 872 -1334 1259 -696 461 -1471 758 -2465 945 -484 90 -1106 133 -1610
            110z"/>
            </g>
      </svg>
      <div class="text">
        {{ commentsLength }}
      </div>
    </div>
    <vue-btn v-if="comments.length" @click="comments.length = 0">Close comments</vue-btn>
    <comments-wrap v-if="comments.length" :comments="comments"/>
  </div>
</template>

<script>
import CommentsWrap from "@/components/commentsWrap";
export default {
  name: "post",
  components: {CommentsWrap},
  data(){
    return{
      commentsLength: '',
      comments: [],
    }
  },
  props: {
    post: {
      type: Object,
    }
  },
  methods: {
    async fetchCommentsLength () {
      try{
        this.isLoading = true;
        fetch(`https://jsonplaceholder.typicode.com/posts/${this.post.id}/comments`)
            .then(response => response.json())
            .then(json => {
              this.commentsLength = json.length
            })

      }
      catch (e) {
        alert('Error')
      } finally {
        this.isLoading = false;
      }
    },
    async fetchComments () {
      try{
        this.isLoading = true;
        fetch(`https://jsonplaceholder.typicode.com/posts/${this.post.id}/comments`)
            .then(response => response.json())
            .then(json => {
              this.comments = json
            })

      }
      catch (e) {
        alert('Error')
      } finally {
        this.isLoading = false;
      }
    },
  },
  mounted() {
    this.fetchCommentsLength();
  }
}
</script>

<style lang="scss" scoped>
  .post{
    border: 2px solid black;
    margin-bottom: 10px;
    padding: 10px;
    width: 100%;
    h3{
      margin-bottom: 10px;
    }
  }
  .post-comments-length{
    width: 30px;
    height: 30px;
    position: relative;
    display: flex;
    cursor: pointer;
    margin-right: 0;
    margin-left: auto;
    margin-top: 5px;
    .text{
      position: absolute;
      top: 49%;
      left: 48%;
      transform: translate(-50%, -50%);
      color: white;
      z-index: 2;

    }
    svg{
      position: absolute;
      z-index: 1;
    }
  }
  button{
    width: fit-content!important;
    margin-right: 0;
    margin-left: auto;
  }
</style>