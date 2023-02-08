<template>
  <TransitionGroup tag="div" name="list" class="tmdb-data">
    <SeriesCard
      v-for="show in tvShows"
      :key="show.id"
      :show="show"
      @tv-show-info="this.$emit('tv-show-info', $event)"
      @overlay-open="this.$emit('overlay-open')"
    />
  </TransitionGroup>
</template>

<script>
import SeriesCard from '../series/SeriesCard.vue';
export default {
  name: 'SeriesList',

  components: {
    SeriesCard,
  },

  props: {
    tvShows: {
      type: Array,
    },
  },
};
</script>

<style lang="scss" scoped>
.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease-in;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(100%);
}
</style>
