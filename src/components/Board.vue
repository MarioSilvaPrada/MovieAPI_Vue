<template>
  <div class="board">
    test
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .board {
    width: 60rem;
    box-shadow: 0 2rem 6rem rgba(0, 0, 0, 0.3);
    height: 40rem;
    border-radius: 1.5rem;
    background: #171934;
    display: flex;
    justify-content: center;
    align-self: center;
    margin: 6rem 0;
  }
</style>
