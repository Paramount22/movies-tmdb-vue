<template>
  <TransitionGroup tag="div" class="tmdb-data" name="list">
    <MovieCard
      v-for="movie in movies"
      :movie="movie"
      :key="movie.id"
      @movie-info="movieAbout($event)"
      @overlay="this.$emit('overlay')"
    />
  </TransitionGroup>
</template>

<script>
import MovieCard from '../movies/MovieCard.vue';
export default {
  name: 'MoviesList',

  emits: ['movie-info', 'overlay'],

  components: {
    MovieCard,
  },

  props: {
    movies: {
      type: Object,
    },
  },

  methods: {
    movieAbout(movie) {
      this.$emit('movie-info', movie);
    },
  },
};
</script>

<style lang="scss" scoped>
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease-in;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(100%);
}
</style>
