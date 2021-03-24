<template>
  <header class="header">
    <b-navbar class="navbar" type="dark" variant="dark">
      <b-container>
        <b-navbar-brand href="#">MovieDB</b-navbar-brand>
        <b-nav-form>
          <b-form-input
            v-model="searchValue"
            class="mr-sm-2 search-input"
            placeholder="Search"
            debounce="500"
          ></b-form-input>
        </b-nav-form>
      </b-container>
    </b-navbar>
  </header>
</template>

<script>
import { mapActions } from "vuex";
export default {
  name: "Header",
  data: () => ({
    searchValue: "",
  }),
  watch: {
    searchValue: "onSerachValueChanged",
  },
  methods: {
    ...mapActions("movies", [
      "searchMovie",
      "fetchMovies",
      "toggleSearchState",
    ]),
    onSerachValueChanged(value) {
      if (value) {
        this.searchMovie(value);
        this.toggleSearchState(true);
      } else {
        this.fetchMovies();
        this.toggleSearchState(false);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.header {
  margin-bottom: 30px;
}

.navbar {
  background-color: rgba(0, 0, 0, 0.6) !important;
}

.search-input {
  color: #c0c0c0 !important;
  background-color: rgba(255, 255, 255, 0.2) !important;
  border-color: rgba(0, 0, 0, 0.5) !important;

  &:focus {
    box-shadow: none;
    background-color: rgba(255, 255, 255, 0.3) !important;
    border-color: rgba(0, 0, 0, 0.3) !important;
  }
}
</style>
