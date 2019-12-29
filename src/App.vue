<template>
  <div id="app">
    <viewer></viewer>
  </div>
</template>

<script>
import Vue from "vue";

import Viewer from "./components/Viewer.vue";

import VueRouter from "vue-router";
Vue.use(VueRouter);

export default {
  name: "app",
  components: {
    Viewer
  }
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
