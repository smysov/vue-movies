<template>
  <div>
    <div class="movie mb-3">
      <div class="movie__poster" :style="posterBacground"></div>
      <div class="movie__info-wrapper">
        <div class="movie__info">
          <h4 class="movie__title">{{ movie.Title }}</h4>
          <span class="movie__year">{{ movie.Year }}</span>
        </div>
        <div class="movie__controls row no-gutters">
          <div class="col">
            <b-button size="md" block variant="outline-light">Edit</b-button>
          </div>
          <div class="col">
            <b-button
              size="md"
              block
              variant="outline-light"
              @click="emitRemoveEvent"
              >Remove</b-button
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieItem",
  props: {
    movie: {
      type: Object,
      required: true,
    },
  },
  computed: {
    posterBacground() {
      return {
        "background-image": `url(${this.movie.Poster})`,
      };
    },
  },
  methods: {
    emitRemoveEvent() {
      this.$emit("removeItem", {
        id: this.movie.imdbID,
        title: this.movie.Title,
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.movie {
  position: relative;
  cursor: pointer;
  border-radius: 5px;
  overflow: hidden;
  transition: 0.3s all ease;
  height: 400px;

  &:hover {
    transform: scale(1.02);
    box-shadow: 0 5px 30px rgba(0, 0, 0, 0.7);

    .movie__info-wrapper {
      opacity: 1;
      background-color: rgba(0, 0, 0, 0.5);
    }
  }

  &__poster {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: center cover no-repeat;
    z-index: -1;
  }

  &__title,
  &__year {
    font-size: 20px;
    color: whitesmoke;
  }

  &__info-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
    padding: 15px 10px;
    opacity: 0;
    transition: opacity 0.3s linear;
  }

  &__controls {
    display: flex;
    column-gap: 10px;
  }
}
</style>
