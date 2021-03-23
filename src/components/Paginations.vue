<template>
  <div class="paginations">
    <b-pagination
      v-model="currentPageModel"
      :perPage="perPage"
      :total-rows="total"
      prev-text="Prev"
      next-text="Next"
    />
  </div>
</template>

<script>
export default {
  name: "MoviesPaginations",
  props: {
    currentPage: {
      type: Number,
      default: 1,
    },
    total: {
      type: Number,
      default: 1,
    },
    perPage: {
      type: Number,
      default: 1,
    },
  },
  computed: {
    currentPageModel: {
      get() {
        return this.currentPage;
      },
      set(value) {
        this.$emit("pageChanged", value);
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.paginations {
  display: flex;
  justify-content: center;
  padding: 20px 0;
}

::v-deep .pagination .page-item .page-link {
  background-color: transparent;
  font-size: 14px;
  color: #fff;
}

::v-deep .pagination .page-item.active .page-link {
  border-color: #fff;
  background-color: #fff;
  color: #000;
}
::v-deep .pagination .page-item.disabled .page-link {
  color: #999999;
}
</style>
