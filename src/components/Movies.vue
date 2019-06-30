<template>
  <div class="movies">
    <div v-if="loading" class="loading">Loading...</div>

    <div v-if="error" class="error">{{ error }}</div>

    <div v-if="movies" class="movies-content">
      <a class="movie" v-for="movie in movies">
        <img v-bind:src="'https://image.tmdb.org/t/p/w300'+ movie.poster_path">
        <p class="movie-title">{{movie.original_title}}</p>
        <p class="movie-genre">{{movie.genre_ids[0]}}</p>
        <span class="rating">{{movie.vote_average}}</span>
        {{moviesData}}
      </a>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Movies",
  data() {
    return {
      loading: false,
      movies: null,
      error: null
    };
  },
  props: ["moviesData"],
  watch: {
    dataMovie: function () {
      console.log(this.moviesData)
    }
  },
  created() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      this.error = this.post = null;
      this.loading = true;

      // switch (moviesData) {
      //   case "popular":
      //     return "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=aeb5dba1f1913a3c858099a94105e7c3&page=1";
      //     break;
      //   case "top_rated":
      //     return "https://api.themoviedb.org/3/movie/top_rated?api_key=aeb5dba1f1913a3c858099a94105e7c3&page=1";
      //     break;
      //   case "theaters":
      //     return "https://api.themoviedb.org/3/movie/now_playing?api_key=aeb5dba1f1913a3c858099a94105e7c3&page=1";
      // } 

      let popular = "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=aeb5dba1f1913a3c858099a94105e7c3&page=1";
      let top_rated = "https://api.themoviedb.org/3/movie/top_rated?api_key=aeb5dba1f1913a3c858099a94105e7c3&page=1";
      let theaters = "https://api.themoviedb.org/3/movie/now_playing?api_key=aeb5dba1f1913a3c858099a94105e7c3&page=1";
      
      axios
        .get(popular)
        .then(res => {
          this.loading = false;
          this.movies = res.data.results;
          //   console.log(res.data.results)
        })
        .catch(err => {
          this.loading = false;
          this.error = err;
        });
    }
  }
};
</script>

<style>
.movies-content {
  display: flex;
  flex-wrap: wrap;
  margin-left: 5rem;
}

.movie {
  margin: 1rem;
}

a {
  width: 11rem;
  position: relative;
}

img {
  width: 10rem;
  border-radius: 0.8rem;
}

.rating {
  background: #faca31;
  color: black;
  font-size: 0.7rem;
  padding: 0.3rem 0.5rem;
  border-radius: 0.3rem;
  position: absolute;
  right: 1rem;
  top: -0.5rem;
}
</style>
