<template>
  <div class="movies-index">
    <div>
      <div class="jumbotron jumbotron-fluid">
        <div class="container" align="center">
          <h1 class="display-4">Movies Index</h1>
          <p class="lead">
            Check out our selection of movies below!
          </p>
        </div>
      </div>
    </div>
    <div>
      <div class="mb-3">
        <label for="exampleFormControlInput1" class="form-label">Search Movies by Title</label>
        <input
          type="text"
          class="form-control"
          id="exampleFormControlInput1"
          placeholder="i.e. Paris is Burning"
          v-model="filter"
        />
      </div>
      <div class="row row-cols-1 row-cols-md-3">
        <div v-for="movie in filterBy(movies, filter, 'title')" v-bind:key="movie.id" class="col mb-4">
          <div class="card">
            <img
              src="https://res.cloudinary.com/people-matters/image/upload/q_auto,f_auto/v1517845732/1517845731.jpg"
              class="card-img-top"
              alt="..."
            />
            <div class="card-body">
              <h5 class="card-title">{{ movie.title }}</h5>
              <p class="card-text">{{ movie.plot }}</p>
              <p class="card-text">Director: {{ movie.director }}</p>
              <p class="card-text">Released: {{ movie.year }}</p>
              <router-link class="btn btn-primary" :to="`/views/movies/${movie.id}`">See movie</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      filter: "",
      sortAttribute: "title",
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
