<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>

      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>

      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="year" />
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="director" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="plot" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
      <small v-if="plot.length > 100" class="red-text">
        Plot cannot exceed 100 characters
      </small>
    </form>
  </div>
</template>

<style scoped>
.red-text {
  color: red;
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
          this.$router.push("/views/movies/index");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
