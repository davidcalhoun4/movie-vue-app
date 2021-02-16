<template>
  <div class="movies-index">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link :to="`/views/movies/${movie.id}`">
      <h2>{{ movie.title }}</h2>
      </router-link>
      <router-link :to="`/movies/${movie.id}`">
        <img v-bind:src="movie.image_url" alt="" />
      </router-link>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>Plot: {{ movie.plot }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>