<template>
  <div class="home">
    <div>
      Title:
      <input type="text" v-model="movieTitle" />
      <br />
      Year:
      <input type="text" v-model="movieYear" />
      <br />
      Director:
      <input type="text" v-model="movieDirector" />
      <br />
      Plot:
      <input type="text" v-model="moviePlot" />
      <br />
      <button v-on:click="createMovie">Create Movie</button>
    </div>

    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>
        <u>{{ movie.title }}</u>
      </h2>
      <p>
        <b>Released:</b>
        {{ movie.year }}
      </p>
      <p>
        <b>Director:</b>
        {{ movie.director }}
      </p>
      <p>
        <b>Plot:</b>
        {{ movie.plot }}
      </p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
// import func from "../../vue-temp/vue-editor-bridge";

export default {
  data: function() {
    return {
      message: "Movies:",
      movies: [],
      movieTitle: "",
      movieYear: "",
      movieDirector: "",
      moviePlot: "",
    };
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
