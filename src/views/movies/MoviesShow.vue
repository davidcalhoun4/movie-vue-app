<template>
  <div class="movies-show">
    <h1>{{ movie.title }}</h1>
    <p>
      <strong>Released:</strong>
      {{ movie.year }}
    </p>
    <img :src="movie.image" class="img-fluid" alt="..." />
    <p>
      <strong>Director:</strong>
      {{ movie.director }}
    </p>
    <p v-if="movie.actors.length > 0">
      <strong>Leading Role Played By:</strong>
      <span v-for="(actor, index) in movie.actors" :key="actor.id">
        {{ actor.first_name }} {{ actor.last_name }}
        <span v-if="index < movie.actors.length - 1">,</span>
      </span>
    </p>
    <p v-if="movie.genres.length > 0">
      <span v-for="(genre, index) in movie.genres" :key="genre.name">
        <strong>Genre:</strong>
        {{ genre }}
        <span v-if="index < movie.genres.length - 1">-</span>
      </span>
    </p>
    <p>
      <strong>Plot:</strong>
      {{ movie.plot }}
    </p>
    <div class="top-buttons" v-if="this.$parent.isLoggedIn()">
      <router-link :to="`/views/movies/${movie.id}/edit`">
        <button class="btn btn-outline-success">Edit Movie</button>
      </router-link>
      <button class="btn btn-outline-danger" v-on:click="destroyMovie()">
        Delete Movie
      </button>
    </div>
  </div>
</template>

<style>
.movies-show {
  margin-top: 20px;
  text-align: center;
}

.img-fluid {
  max-width: 50%;
  margin-bottom: 20px;
}
</style>

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
