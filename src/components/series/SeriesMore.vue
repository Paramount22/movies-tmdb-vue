<template>
  <div class="more-data" v-if="tvShows.length">
    <button
      class="more"
      v-show="visibilityBtn"
      @click.prevent="this.$emit('more-series')"
    >
      More
    </button>
  </div>

  <div class="more-data" v-if="tvShows.length">
    <button
      class="more"
      v-show="visibilityBtnSearch && tvShows.length != totalResults"
      @click.prevent="this.$emit('more-searched-series')"
    >
      More
    </button>
  </div>
</template>

<script>
export default {
  name: 'SeriesMore',

  emits: ['more-series', 'more-searched-series'],

  props: {
    tvShows: {
      type: Array,
    },

    totalResults: {
      type: Number,
    },

    visibilityBtn: {
      type: Boolean,
    },
    visibilityBtnSearch: {
      type: Boolean,
    },
  },
};
</script>

<style lang="scss" scoped></style>
