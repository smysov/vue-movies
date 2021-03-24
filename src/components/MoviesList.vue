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
          />
        </b-col>
      </template>
      <template v-else>
        <div>Empty List</div>
      </template>
    </b-row>
  </b-container>
</template>

<script>
import { mapActions, mapGetters } from "vuex";
import movieItem from "@/components/MovieItem.vue";

export default {
  name: "MoviesList",
  components: { movieItem },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  computed: {
    ...mapGetters("movies", ["isSearch"]),
    isExist() {
      return Boolean(Object.keys(this.list).length);
    },
    listTitle() {
      return this.isSearch ? "Search result" : "IMDB Top 250";
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
