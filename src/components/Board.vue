<template>
  <div class="board">
    <SideBar v-bind:genres="genres"/>
    <Movies/>
  </div>
</template>

<script>
import axios from "axios";

import SideBar from "./SideBar";
import Movies from "./Movies";

export default {
  name: "Board",
  components: {
    SideBar,
    Movies
  },
  data() {
    return {
      genres: {
        loading: false,
        genres: null,
        error: null
      }
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
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.board {
  width: 60rem;
  box-shadow: 0 2rem 6rem rgba(0, 0, 0, 0.3);
  border-radius: 1.5rem;
  background: #171934;
  display: flex;
  justify-content: center;
  align-self: center;
  margin: 6rem 0;
  color: white;
}

.error,
.loading,
.post {
  display: flex;
  align-self: center;
}
</style>
