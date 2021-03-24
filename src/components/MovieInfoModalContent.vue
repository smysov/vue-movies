<template>
  <div class="movie-info">
    <div class="movie-info__wrapper">
      <header class="movie-info__header">
        <h4 class="movie-info__title">Movie view</h4>
        <b-icon-x class="movie-info__close" @click="closeModal" />
      </header>
      <div class="movie-info__content">
        <b-row>
          <b-col sm="4">
            <div class="movie-info__wrapper-poster">
              <div class="movie-info__poster" :style="posterStyle"></div>
            </div>
          </b-col>
          <b-col sm="8">
            <h5 class="movie-info__name-movie">{{ movie.Title }}</h5>
            <b-form-rating
              class="movie-info__rating"
              v-model="movie.imdbRating"
              readonly
              show-value
              precision="1"
              stars="10"
              show-value-max
              no-border
            />
            <p class="movie-info__description">{{ movie.Plot }}</p>
            <div class="movie-info__badge">
              <b-badge class="mr-2" variant="success">{{ movie.Year }}</b-badge>
              <b-badge class="mr-2" variant="success">{{
                movie.Runtime
              }}</b-badge>
              <b-badge class="mr-2" variant="success">{{
                movie.Language
              }}</b-badge>
            </div>
            <table class="table small">
              <tbody>
                <tr>
                  <th>Production</th>
                  <td>{{ movie.Production }}</td>
                </tr>
                <tr>
                  <th>Country</th>
                  <td>{{ movie.Country }}</td>
                </tr>
                <tr>
                  <th>Director</th>
                  <td>{{ movie.Director }}</td>
                </tr>
                <tr>
                  <th>Writer</th>
                  <td>{{ movie.Writer }}</td>
                </tr>
                <tr>
                  <th>Actors</th>
                  <td>{{ movie.Actors }}</td>
                </tr>
                <tr>
                  <th>Awards</th>
                  <td>{{ movie.Awards }}</td>
                </tr>
              </tbody>
            </table>
          </b-col>
        </b-row>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalInfoContent",
  props: {
    movie: {
      type: Object,
      required: true,
    },
  },
  data: () => ({
    defaultPoster:
      "linear-gradient(45deg, rgb(0, 3, 38) 0%, rgb(82, 15, 117) 100%)",
  }),
  computed: {
    posterStyle() {
      return {
        "background-image": this.posterBackground,
      };
    },
    posterBackground() {
      return this.movie ? `url(${this.movie.Poster})` : this.defaultPoster;
    },
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
  },
};
</script>

<style lang="scss" scoped>
.movie-info {
  &__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    background: linear-gradient(45deg, rgb(0, 3, 38) 0%, rgb(82, 15, 117) 100%);
    color: #fff;
  }

  &__title {
    margin-bottom: 0;
    line-height: 1.5;
    font-size: 1.25rem;
  }

  &__content {
    padding: 1rem;
    background-color: #fff;
  }

  &__wrapper-poster {
    position: relative;
    padding-bottom: 150%;
    border-radius: 5px;
    overflow: hidden;
    transition: all 0.3s ease;
  }

  &__poster {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-position: center center;
    background-size: cover;
  }

  &__name-movie {
    font-size: 24px;
    font-weight: 300;
    line-height: 1.2;
    margin-top: 10px;

    @media (min-width: 480px) {
      font-size: 28px;
    }
  }

  &__rating {
    padding: 0;
  }

  &__rating:focus {
    box-shadow: none;
  }

  &__badge {
    margin: 10px 0;
  }

  &__description {
    font-size: 14px;
    font-weight: 300;

    @media (min-width: 480px) {
      font-size: 18px;
    }
  }

  &__close {
    font-size: 24px;
    cursor: pointer;
  }
}
.movie-info__rating::v-deep .b-rating-star,
.movie-info__rating::v-deep .b-rating-value {
  justify-content: flex-start;
  flex-grow: 0 !important;
  font-size: 16px;
  font-weight: 300;
  padding: 0;

  @media (min-width: 480px) {
    font-size: 20px;
  }
}

.movie-info__rating::v-deep .b-rating-star + .b-rating-star {
  margin-left: 2px;

  @media (min-width: 480px) {
    margin-left: 4px;
  }
}

.movie-info__rating::v-deep .b-rating-value {
  margin-left: 10px;
}

.movie-info__rating::v-deep .b-rating-star .b-rating-icon {
  color: #ffc107;
}

#movie-info .modal .fade .show {
  padding: 20px !important;
}
</style>
