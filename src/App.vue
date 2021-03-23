<template>
  <div id="app">
    <movies-list :list="moviesList" />
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import moviesList from "@/components/MoviesList.vue";

export default {
  name: "App",
  components: { moviesList },
  computed: {
    ...mapGetters("movies", ["moviesList"]),
  },
  methods: {
    ...mapActions("movies", ["fetchMovies"]),
  },
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
