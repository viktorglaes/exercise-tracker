<template>
  <div id="app" class="parent-app">
    <section class="hero is-success">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            Exercise Tracking
          </h1>
          <h2 class="subtitle">
            Easily track your exercises with style
          </h2>
        </div>
      </div>
    </section>
    <Dashboard />
    <Tracker />
  </div>
</template>

<script>
import Dashboard from "./components/Dashboard.vue";
import Tracker from "./components/Tracker.vue";

export default {
  name: "App",
  components: {
    Dashboard,
    Tracker,
  },
};
</script>

<style>
.parent-app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
