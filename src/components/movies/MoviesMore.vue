<template>
  <div class="more-data" v-show="searchedMovie === false">
    <button
      class="more"
      v-show="popularMoviesActive()"
      v-if="movies.length"
      @click.prevent="this.$emit('more-popular-movies')"
    >
      More
    </button>

    <button
      class="more"
      v-show="topRatedMoviesActive()"
      v-if="movies.length"
      @click.prevent="this.$emit('more-top-rated-movies')"
    >
      More
    </button>

    <button
      class="more"
      v-show="upcomingMoviesActive()"
      v-if="movies.length"
      @click.prevent="this.$emit('more-upcoming-movies')"
    >
      More
    </button>
  </div>
</template>

<script>
export default {
  name: 'MoviesMore',

  emits: [
    'more-popular-movies',
    'more-top-rated-movies',
    'more-upcoming-movies',
  ],

  props: {
    movies: {
      type: Array,
    },

    searchedMovie: {
      type: Boolean,
    },
  },

  methods: {
    popularMoviesActive() {
      const filterLinks = document.querySelectorAll('.filter a');
      if (filterLinks[0].classList.contains('active')) {
        return true;
      }
    },

    topRatedMoviesActive() {
      const filterLinks = document.querySelectorAll('.filter a');
      if (filterLinks[1].classList.contains('active')) {
        return true;
      }
    },

    upcomingMoviesActive() {
      const filterLinks = document.querySelectorAll('.filter a');
      if (filterLinks[2].classList.contains('active')) {
        return true;
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
