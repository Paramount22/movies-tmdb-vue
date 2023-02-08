<template>
  <div
    class="tmdb-data-card"
    @click="
      //overlay = true;
      this.$emit('movie-info', movie);
      this.$emit('overlay');
    "
  >
    <img
      class="tmdb-data-poster"
      :src="`${IMG_PATH}${movie.poster_path}`"
      :alt="movie.title"
    />

    <h4 class="tmdb-data-title">{{ movie.title }}</h4>

    <div class="tmdb-data-rating" :class="getClassByRating(movie.vote_average)">
      {{ ratingToPercentage(movie.vote_average) }}%
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieCard',

  emits: ['movie-info', 'overlay'],

  props: {
    movie: {
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

    // genres divided by /
    divider(genres) {
      return this.modifiedGenres(genres).join(' / ');
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
