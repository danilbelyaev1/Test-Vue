<template>
  <button class="btn"><slot/></button>
</template>

<script>
export default {
  name: "vueBtn"
}
</script>

<style scoped>
  .btn{
    color: white;
    padding: 10px 20px;
    width: 100%;
    background: black;
    display: flex;
    cursor: pointer;
    text-align: center;
    justify-content: center;
    margin-top: 10px;
  }
</style>