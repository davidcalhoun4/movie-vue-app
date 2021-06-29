<template>
  <div class="home">
    <div class="jumbotron jumbotron-fluid">
      <div class="container" align="center">
        <h1 class="display-4">Welcome to Movies</h1>
        <p class="lead">
          ..
        </p>
      </div>
    </div>
    <div align="center">
      <img src="https://media.timeout.com/images/101713011/630/472/image.jpg" alt="" />
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
// import func from "../../vue-temp/vue-editor-bridge";

export default {
  data: function() {
    return {};
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function() {
      var params = {
        title: this.movieTitle,
        year: this.movieYear,
        director: this.movieDirector,
        plot: this.moviePlot,
      };
      axios
        .post("/api/movies", params, {
          headers: {
            Authorization: "Bearer jwt",
          },
        })
        .then(response => {
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data);
        });
    },
  },
};
</script>
