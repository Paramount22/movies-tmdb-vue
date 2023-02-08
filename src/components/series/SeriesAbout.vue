<template>
  <Transition name="scale">
    <div class="overlay" v-if="overlay">
      <section class="about-series">
        <img
          class="tmdb-data-poster"
          :src="`${IMG_PATH}${seriesInfo.poster_path}`"
          :alt="seriesInfo.name"
        />
        <article class="about">
          <header class="about-header">
            <h2>{{ seriesInfo.name }}</h2>
            <div
              class="tmdb-data-rating"
              :class="getClassByRating(seriesInfo.vote_average)"
            >
              {{ ratingToPercentage(seriesInfo.vote_average) }}%
            </div>
          </header>

          <p>{{ seriesInfo.overview }}</p>
          <p>{{ seriesInfo.original_language }}</p>
          <p>{{ dateTransform(seriesInfo.first_air_date) }}</p>

          <p>{{ divider(seriesInfo.genre_ids) }}</p>
        </article>
        <div class="close-about-series" @click="this.$emit('overlay-close')">
          X
        </div>
      </section>
    </div>
  </Transition>
</template>

<script>
import { allgenresId } from '../../genres';
export default {
  name: 'SeriesAbout',

  props: {
    seriesInfo: {
      type: Object,
    },

    overlay: {
      type: Boolean,
    },
  },

  data() {
    return {
      IMG_PATH: 'https://image.tmdb.org/t/p/w1280',
    };
  },

  methods: {
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

    // convert to percentage
    ratingToPercentage(rating) {
      return rating * 10;
    },

    // modify date only to Year
    dateTransform(date) {
      return date.slice(0, 4);
    },

    // genres divided by /
    divider(genres) {
      return this.modifiedGenres(genres).join(' / ');
    },

    modifiedGenres(genres) {
      return genres.map((genre) => allgenresId(genre));
    },
  },
};
</script>

<style lang="scss" scoped>
.scale-enter-active,
.scale-leave-active {
  transition: all 0.2s ease-out;
}

.scale-enter-from,
.scale-leave-to {
  opacity: 0;
  transform: scale(0.75);
}
</style>
