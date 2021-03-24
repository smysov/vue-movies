<template>
  <div id="app">
    <loader />
    <notifications />
    <poster-background :poster="posterBackground" />
    <Header />
    <movies-list :list="moviesList" @changePoster="onChangePoster" />
    <paginations
      :current-page="currentPage"
      :per-page="moviesPerPage"
      :total="moviesLength"
      @pageChanged="onPageChanged"
    />
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import moviesList from "@/components/MoviesList";
import posterBackground from "@/components/PosterBackground";
import paginations from "@/components/Paginations";
import loader from "@/components/Loader";
import Header from "@/components/Header";
import notifications from "@/components/Notifications";

export default {
  name: "App",
  components: {
    moviesList,
    posterBackground,
    paginations,
    loader,
    Header,
    notifications,
  },
  data: () => ({
    posterBackground: "",
  }),
  computed: {
    ...mapGetters("movies", [
      "moviesList",
      "currentPage",
      "moviesPerPage",
      "moviesLength",
    ]),
  },
  watch: {
    "$route.query": {
      handler: "onPageQueryChange",
      immediate: true,
      deep: true,
    },
  },
  methods: {
    ...mapActions("movies", ["fetchMovies", "changeCurrentPage"]),
    onPageQueryChange({ page = 1 }) {
      this.changeCurrentPage(Number(page));
    },
    onChangePoster(poster) {
      this.posterBackground = poster;
    },
    onPageChanged(page) {
      this.$router.push({ query: { page } });
    },
  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  position: relative;
  font-family: Arial, Helvetica, sans-serif;
  min-height: 100vh;
}
</style>
