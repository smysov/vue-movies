<template>
  <div id="app">
    <poster-background :poster="posterBackground" />
    <movies-list :list="moviesList" @changePoster="onChangePoster" />
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import moviesList from "@/components/MoviesList";
import posterBackground from "@/components/PosterBackground";

export default {
  name: "App",
  components: { moviesList, posterBackground },
  data: () => ({
    posterBackground: "",
  }),
  computed: {
    ...mapGetters("movies", ["moviesList"]),
  },
  methods: {
    ...mapActions("movies", ["fetchMovies"]),
    onChangePoster(poster) {
      this.posterBackground = poster;
    },
  },
};
</script>

<style>
#app {
  position: relative;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
