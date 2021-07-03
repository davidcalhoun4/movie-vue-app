<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="/">
          <div>
            <span style="color:#ff0000;">Q</span>
            <span style="color:#ff4000;">u</span>
            <span style="color:#ff7f00;">e</span>
            <span style="color:#f3b306;">e</span>
            <span style="color:#e7e70b;">r</span>
            <span style="color:#00ff00;"></span>
            <span style="color:#00ff80;">F</span>
            <span style="color:#00ffff;">l</span>
            <span style="color:#0080ff;">i</span>
            <span style="color:#0000ff;">x</span>
          </div>
        </a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNavAltMarkup"
          aria-controls="navbarNavAltMarkup"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
          <div class="navbar-nav">
            <router-link class="nav-link" to="/views/movies/index">Movie Index</router-link>
            <router-link class="nav-link" v-if="isLoggedIn()" to="/views/movies/new">Create Movie</router-link>
            <router-link class="nav-link" v-if="!isLoggedIn()" to="/signup">- Signup -</router-link>
            <router-link class="nav-link" v-if="!isLoggedIn()" to="/login">- Login -</router-link>
            <router-link class="nav-link" v-if="isLoggedIn()" to="/logout">- Logout -</router-link>
          </div>
        </div>
      </div>
    </nav>

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
    getUserId: function() {
      return localStorage.user_id;
    },
  },
};
</script>
