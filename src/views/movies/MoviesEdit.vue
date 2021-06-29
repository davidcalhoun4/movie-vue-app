<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovie()">
      <h1>Edit Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>

      <div class="mb-3">
        <label class="form-label">Title</label>
        <input type="text" class="form-control" id="title" aria-describedby="nameHelp" v-model="movie.title" />
      </div>
      <div class="mb-3">
        <label class="form-label">Year</label>
        <input type="text" class="form-control" id="year" aria-describedby="nameHelp" v-model="movie.year" />
      </div>
      <div class="mb-3">
        <label class="form-label">Director</label>
        <input type="text" class="form-control" id="director" aria-describedby="nameHelp" v-model="movie.director" />
      </div>
      <div class="mb-3">
        <label class="form-label">Plot</label>
        <textarea rows="5" class="form-control" id="plot" aria-describedby="nameHelp" v-model="movie.plot"></textarea>
      </div>
      <input type="submit" class="btn btn-primary" value="Update" />
    </form>
  </div>
</template>

<style>
.movies-edit {
  margin-top: 20px;
}
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: {},
      errors: [],
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      this.movie = response.data;
      console.log(this.movie);
    });
  },
  methods: {
    updateMovie: function() {
      var params = {
        title: this.movie.title,
        year: this.movie.year,
        director: this.movie.director,
        plot: this.movie.plot,
      };
      axios
        .patch(`/api/movies/${this.movie.id}`, params)
        .then(response => {
          console.log(response.data);
          this.$router.push(`/views/movies/${this.movie.id}`);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
