<template>
  <div class="movies-index">
    <div>
      <div class="jumbotron jumbotron-fluid">
        <div class="container" align="center">
          <h6 class="display-4">
            <div>
              <span style="color:#ff0000;">B</span>
              <span style="color:#ff2000;">r</span>
              <span style="color:#ff4000;">o</span>
              <span style="color:#ff5f00;">w</span>
              <span style="color:#ff7f00;">s</span>
              <span style="color:#fa9a00;">e</span>
              <span style="color:#f6b600;"></span>
              <span style="color:#f1d100;">Q</span>
              <span style="color:#ecec00;">u</span>
              <span style="color:#b1f100;">e</span>
              <span style="color:#76f600;">e</span>
              <span style="color:#3bfa00;">r</span>
              <span style="color:#00ff00;"></span>
              <span style="color:#00ff40;">C</span>
              <span style="color:#00ff80;">l</span>
              <span style="color:#00ffbf;">a</span>
              <span style="color:#00ffff;">s</span>
              <span style="color:#00bfff;">s</span>
              <span style="color:#0080ff;">i</span>
              <span style="color:#0040ff;">c</span>
              <span style="color:#0000ff;">s</span>
            </div>
          </h6>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="row justify-content-md-center">
        <div class="col-md-auto">
          <!-- <div class="mb-3"> -->
          <!-- <label for="exampleFormControlInput1" class="form-label">Search Movies by Title</label> -->
          <br />
          <input
            type="text"
            class="form-control"
            id="exampleFormControlInput1"
            placeholder="Search by Title"
            v-model="searchTerm"
          />
          <!-- </div> -->
        </div>
        <div class="col-md-auto">
          <br />
          <button type="button" class="btn btn-outline-secondary" v-on:click="setSortAttribute('title')">
            Sort by Title
          </button>
        </div>
        <div class="col-md-auto">
          <br />
          <button type="button" class="btn btn-outline-secondary" v-on:click="setSortAttribute('year')">
            Sort by Year Released
          </button>
        </div>
      </div>
    </div>
    <hr />
    <div class="row row-cols-1 row-cols-md-3">
      <div
        v-for="movie in filterBy(orderBy(movies, sortAttribute, sortOder), searchTerm, 'title')"
        v-bind:key="movie.id"
        class="col mb-4"
      >
        <div class="card">
          <img :src="movie.image" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">
              <span class="text">{{ movie.plot }}</span>
            </p>
            <p class="card-text">
              <strong>Director:</strong>
              {{ movie.director }}
            </p>
            <p class="card-text">
              <strong>Released:</strong>
              {{ movie.year }}
            </p>
            <!-- <p class="card-text" v-for="genre in movie.genres" :key="genre.name">{{ genre }}</p> -->
            <p v-if="movie.genres.length > 0">
              <strong>Genre:</strong>
              <span v-for="(genre, index) in movie.genres" :key="genre.name">
                {{ genre }}
                <span v-if="index < movie.genres.length - 1">-</span>
              </span>
            </p>
            <router-link class="btn btn-outline-primary" :to="`/movies/${movie.id}`">View Movie</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
/* .btn btn-secondary {
  margin-right: 20px;
} */
.text {
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      searchTerm: "",
      sortAttribute: "year",
      sortOder: 1,
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {
    setSortAttribute: function(attribute) {
      if (attribute === this.sortAttribute) {
        this.sortOder = this.sortOder * -1;
      } else {
        this.sortOder = 1;
      }
      this.sortAttribute = attribute;
    },
  },
};
</script>
