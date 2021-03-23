<template>
  <div class="poster" :style="posterStyle"></div>
</template>

<script>
export default {
  name: "PosterBackground",
  data: () => ({
    defaultPoster:
      "linear-gradient(45deg, rgb(0, 3, 38) 0%, rgb(82, 15, 117) 100%)",
  }),
  props: {
    poster: {
      type: String,
      default: "",
    },
  },
  computed: {
    posterStyle() {
      return {
        "background-image": this.posterBackground,
      };
    },
    posterBackground() {
      return this.poster ? `url(${this.poster})` : this.defaultPoster;
    },
  },
};
</script>

<style lang="scss" scoped>
.poster {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
  background-size: cover;
  background-position: center;
  transition: 0.3s all ease;

  &::before {
    position: absolute;
    content: "";
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    opacity: 0.5;
    background-image: linear-gradient(
      45deg,
      rgb(0, 3, 38) 0%,
      rgb(82, 15, 117) 100%
    );
  }
}
</style>
