<template>
  <div class="container">
    <Board/>
  </div>
</template>

<script>
// @ is an alias to /src
import Board from "@/components/Board.vue";

export default {
  name: "home",
  components: {
    Board
  }
};
</script>

<style >
@import "../config/style.js";

.container {
  background: #7f7fd5; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #91eae4,
    #86a8e7,
    #7f7fd5
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #91eae4,
    #86a8e7,
    #7f7fd5
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

