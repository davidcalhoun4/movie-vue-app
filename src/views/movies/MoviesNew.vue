<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>

      <div class="mb-3">
        <label class="form-label">Title</label>
        <input type="text" class="form-control" id="title" aria-describedby="nameHelp" v-model="title" />
      </div>
      <div class="mb-3">
        <label class="form-label">Year</label>
        <input type="text" class="form-control" id="year" aria-describedby="nameHelp" v-model="year" />
      </div>
      <div class="mb-3">
        <label class="form-label">Director</label>
        <input type="text" class="form-control" id="director" aria-describedby="nameHelp" v-model="director" />
      </div>
      <div class="mb-3">
        <label class="form-label">Plot</label>
        <textarea rows="5" class="form-control" id="plot" aria-describedby="nameHelp" v-model="plot">Hello</textarea>
        <small v-if="plot.length < 30" class="red-text">
          Plot must be more than 30 characters
        </small>
      </div>
      <input type="submit" class="btn btn-outline-primary" value="Create" />
    </form>
  </div>
</template>

<style scoped>
.red-text {
  color: red;
}

.movies-new {
  margin-top: 20px;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      year: "",
      director: "",
      plot: "",
      errors: [],
    };
  },
  methods: {
    createMovie: function() {
      var params = {
        title: this.title,
        year: this.year,
        director: this.director,
        plot: this.plot,
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          console.log(response.data);
          this.$router.push("/movies/index");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
