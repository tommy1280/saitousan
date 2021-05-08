<template>
  <div id="app">
    <div>
      <router-view />
    </div>
    <div>
      <router-link to="/" class="btn btn-dark mt-5">Home</router-link>

      <router-link to="/playgame" class="btn btn-dark mt-5"
        >PlayGame</router-link
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
