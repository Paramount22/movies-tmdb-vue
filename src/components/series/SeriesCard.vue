<template>
  <div
    class="tmdb-data-card"
    @click="this.$emit('tv-show-info', show), this.$emit('overlay-open')"
  >
    <img
      class="tmdb-data-poster"
      :src="`${IMG_PATH}${show.poster_path}`"
      alt=""
    />

    <h4 class="tmdb-data-title">
      {{ show.name }}
    </h4>

    <div class="tmdb-data-rating" :class="getClassByRating(show.vote_average)">
      {{ ratingToPercentage(show.vote_average) }}%
    </div>
  </div>
</template>

<script>
export default {
  name: 'SeriesCard',

  props: {
    show: {
      type: Object,
    },
  },

  data() {
    return {
      IMG_PATH: 'https://image.tmdb.org/t/p/w1280',
    };
  },

  methods: {
    // convert to percentage
    ratingToPercentage(rating) {
      return rating * 10;
    },

    // class by rating
    getClassByRating(rating) {
      if (rating >= 7) {
        return 'red';
      } else if (rating >= 4) {
        return 'blue';
      } else if (rating > 0) {
        return 'gray';
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
