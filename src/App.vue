<template>
  <div id="app">
    <div id="nav">
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="/">Movies App</a>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNavAltMarkup"
          aria-controls="navbarNavAltMarkup"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
          <div class="navbar-nav">
            <!-- <router-link class="nav-link" to="/">Home</router-link> -->
            <router-link class="nav-link" v-if="isLoggedIn()" to="/logout">Logout</router-link>
            <router-link class="nav-link" v-if="!isLoggedIn()" to="/signup">Signup</router-link>
            <router-link class="nav-link" v-if="!isLoggedIn()" to="/login">Login</router-link>
            <router-link class="nav-link" v-if="isLoggedIn()" to="/views/movies/index">Movies Index</router-link>
            <router-link class="nav-link" v-if="isLoggedIn()" to="/views/movies/new">Create Movie</router-link>
          </div>
        </div>
      </nav>
    </div>
    <div class="container">
      <!-- Content here -->
      <router-view />
    </div>
    <!-- <router-view /> -->
  </div>
</template>

<script>
export default {
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
