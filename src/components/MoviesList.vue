<template>
  <b-container>
    <h3 class="title">{{ listTitle }}</h3>
    <b-row>
      <template v-if="isExist">
        <b-col v-for="(movie, key) in list" :key="key">
          <movie-item
            :movie="movie"
            @mouseover.native="onMouseOver(movie.Poster)"
            @removeItem="onRemoveItem"
            @showModal="onShowMovieInfo"
          />
        </b-col>
      </template>
      <template v-else>
        <div>Empty List</div>
      </template>
    </b-row>
    <b-modal
      body-class="movie-modal-body"
      :id="movieInfoModalID"
      size="xl"
      hide-footer
      hide-header
      style="padding: 20px"
    >
      <movie-info-modal-content
        :movie="selectedMovie"
        @closeModal="onCloseModal"
      />
    </b-modal>
  </b-container>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import movieItem from "@/components/MovieItem";
import movieInfoModalContent from "@/components/MovieInfoModalContent";

export default {
  name: "MoviesList",
  components: { movieItem, movieInfoModalContent },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  data: () => ({
    movieInfoModalID: "movie-info",
    selectedMovieID: "",
  }),
  computed: {
    ...mapGetters("movies", ["isSearch"]),
    isExist() {
      return Boolean(Object.keys(this.list).length);
    },
    listTitle() {
      return this.isSearch ? "Search result" : "IMDB Top 250";
    },
    selectedMovie() {
      return this.selectedMovieID ? this.list[this.selectedMovieID] : {};
    },
  },
  methods: {
    ...mapActions("movies", ["removeMovie"]),
    ...mapActions(["showNotify"]),
    onMouseOver(poster) {
      this.$emit("changePoster", poster);
    },
    async onRemoveItem({ id, title }) {
      const isConfirmed = await this.$bvModal.msgBoxConfirm(
        `Are you sure delete this movie ${title}?`
      );

      if (isConfirmed) {
        this.removeMovie(id);
        this.showNotify({
          msg: "Movie deleted successful",
          title: "Success",
          variant: "success",
        });
      }
    },
    onShowMovieInfo(id) {
      this.selectedMovieID = id;
      this.$bvModal.show(this.movieInfoModalID);
    },
    onCloseModal() {
      this.selectedMovieID = null;
      this.$bvModal.hide(this.movieInfoModalID);
    },
  },
};
</script>

<style lang="scss" scoped>
.title {
  font-size: 22px;
  margin-bottom: 50px;
  color: rgba(255, 255, 255, 0.7);

  @media (min-width: 768px) {
    font-size: 32px;
  }
}

.row {
  display: flex;
  justify-content: center;
}

.col {
  min-width: 295px;
  max-width: 325px;
}
</style>

<style>
.movie-modal-body {
  padding: 0 !important;
}

div#movie-info.modal.fade.show {
  padding: 15px !important;
}
</style>
