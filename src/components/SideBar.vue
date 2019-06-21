<template>
  <div class="side-bar">
    <div v-if="genres.loading" class="loading">Loading...</div>

    <div v-if="genres.error" class="error">{{ error }}</div>

    <div v-if="genres.genres" class="content">
      <p v-for="genre in genres.genres" v-on:click="onClick(genre.id)">{{genre.name}}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SideBar",
  props: ['genres'],
  methods: {
    onClick(id) {
      console.log(id);
    }
  }
};
</script>

<style scoped>
.content {
  height: 30rem;
  overflow-y: scroll;
  width: 10rem;
}

p {
  cursor: pointer;
}
</style>
