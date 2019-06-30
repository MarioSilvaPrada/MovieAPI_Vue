<template>
  <div class="board">
    <select name="movieData" v-on:change="sortValue">
      <option value="popular" selected>Popular</option>
      <option value="top_rated">Top Rated</option>
      <option value="theaters">Theaters</option>
    </select>
    <div class="movies">
      <SideBar v-bind:genres="genres"/>
      <Movies v-bind:moviesData="moviesData"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";

import SideBar from "./SideBar";
import Movies from "./Movies";
import Header from "./Header";

export default {
  name: "Board",
  components: {
    SideBar,
    Movies,
    Header
  },
  data() {
    return {
      genres: {
        loading: false,
        genres: null,
        error: null
      },
      moviesData: ""
    };
  },
  created() {
    this.fetchGenres();
  },
  methods: {
    fetchGenres() {
      this.genres.error = this.genres.genres = null;
      this.genres.loading = true;

      let API_URL = "https://api.themoviedb.org/3/";
      let API_KEY = "?api_key=aeb5dba1f1913a3c858099a94105e7c3";

      axios
        .get(`${API_URL}genre/movie/list${API_KEY}`)
        .then(res => {
          this.genres.loading = false;
          this.genres.genres = res.data.genres;
          // console.log(res.data.genres)
        })
        .catch(err => {
          this.genres.loading = false;
          this.genres.error = err;
        });
    },
    sortValue(e) {
      this.moviesData = e.target.value
      // console.log(e.target.value)
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board {
  width: 70rem;
  box-shadow: 0 2rem 6rem rgba(0, 0, 0, 0.3);
  border-radius: 1.5rem;
  background: #171934;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-self: center;
  margin: 6rem 0;
  color: white;
}

.movies {
  display: flex;
}

.error,
.loading,
.post {
  display: flex;
  align-self: center;
}
</style>
