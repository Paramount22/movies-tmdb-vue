<template>
  <main>
    <MoviesApp @overlay="overlay = true" @about-movie="movieInfo = $event" />
  </main>

  <MoviesAbout
    :movie-info="movieInfo"
    :overlay="overlay"
    @overlay-close="overlay = false"
  />
</template>

<script>
import MoviesApp from '../components/movies/MoviesApp.vue';
import MoviesAbout from '../components/movies/MoviesAbout.vue';
export default {
  components: {
    MoviesApp,
    MoviesAbout,
  },

  data() {
    return {
      movieInfo: {},
      overlay: false,
    };
  },
};
</script>

<style lang="scss" scoped></style>
