<template>
  <b-container>
    <h3 class="title">IMDB Top 250</h3>
    <b-row>
      <template v-if="isExist">
        <b-col v-for="(movie, key) in list" :key="key">
          <movie-item :movie="movie" />
        </b-col>
      </template>
      <template v-else>
        <div>Empty List</div>
      </template>
    </b-row>
  </b-container>
</template>
<script>
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
    isExist() {
      return Boolean(Object.keys(this.list).length);
    },
  },
};
</script>

<style lang="scss" scoped>
.title {
  font-size: 22px;
  margin-bottom: 50px;

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
