<template>
  <div class="movies-index">
    <div>
      <div>
        <button v-on:click="sortAttribute = 'title'">
          Sort by title
        </button>
      </div>
    </div>
    <div>
      Search by title: <input type="text" v-model="titleFilter" list="titles" />
      <datalist id="titles">
        <option v-for="movie in movies" v-bind:key="movie.id"
          >{{ movie.title }}
        </option>
      </datalist>
    </div>
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
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      titleFilter: "",
      orderAttribute: "title",
    };
  },
  created: function() {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
