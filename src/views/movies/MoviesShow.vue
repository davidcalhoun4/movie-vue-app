<template>
  <div class="movies-show">
    <h1>{{ movie.title }}</h1>
    <p>Year: {{ movie.year }}</p>
    <p>Director: {{ movie.director }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <div class="top-buttons" v-if="this.$parent.isLoggedIn()">
      <router-link :to="`/views/movies/${movie.id}/edit`">
        <button class="btn btn-success">Edit Movie</button>
      </router-link>
      <button class="btn btn-danger ml-3" v-on:click="destroyMovie()">
        Delete Movie
      </button>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: {},
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      this.movie = response.data;
      console.log(this.movie);
    });
  },
  methods: {
    destroyMovie: function() {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/api/movies/${this.movie.id}`).then(response => {
          console.log(response.data);
          this.$router.push("/views/movies/index");
        });
      }
    },
  },
};
</script>
