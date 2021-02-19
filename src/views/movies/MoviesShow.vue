<template>
  <div class="movies-show">
    <h1>{{ movie.title }}</h1>
    <p>Year: {{ movie.year }}</p>
    <p>Director: {{ movie.director }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <router-link :to="`/views/movies/${movie.id}/edit`">
    <button>Edit</button>
    </router-link>
    <button v-on:click="destroyRecipe()">Delete</button>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get(`/api/movies/${this.$route.params.id}`).then((response) => {
      this.movie = response.data;
      console.log(this.movie);
    });
  },
  methods: {
    destroyRecipe: function () {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/api/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/views/movies/index");
        });
      }
    },
  },
};
</script>