<template>
  <LoadingIcon :loading="loading" />

  <div class="tmdb-data-filter">
    <MoviesFilter
      @get-movies="getMovies"
      @get-top-rated-movies="getTopRatedMovies"
      @get-upcoming-movies="getUpcomingMovies"
    />
    <MoviesSearch
      @searchedQuery="query = $event"
      @form-submitted="getMoviesBySearch"
      @start-search="searchedMovie = true"
    />
  </div>

  <NotFound :message="message" />

  <MoviesList
    :movies="movies"
    @movie-info="movieAbout($event)"
    @overlay="this.$emit('overlay')"
  />

  <MoviesMore
    :movies="movies"
    @more-popular-movies="getMorePopularMovies"
    @more-top-rated-movies="getMoreTopRatedMovies"
    @more-upcoming-movies="getMoreUpcomingMovies"
    :searchedMovie="searchedMovie"
  />
</template>

<script>
import axios from 'axios';
import MoviesList from '../movies/MoviesList.vue';
import MoviesFilter from '../movies/MoviesFilter.vue';
import MoviesMore from '../movies/MoviesMore.vue';
import MoviesSearch from '../movies/MoviesSearch.vue';
import LoadingIcon from '../LoadingIcon.vue';
import NotFound from '../NotFound.vue';
export default {
  name: 'MoviesApp',
  components: {
    MoviesList,
    MoviesFilter,
    MoviesMore,
    MoviesSearch,
    LoadingIcon,
    NotFound,
  },

  data() {
    return {
      movies: [],
      overlay: false,
      loading: false,
      page: 1,
      query: '',
      searchedMovie: false,
      apiKey: '8335b966aa0001f618384081f205b83d',
      message: '',
    };
  },
  emits: ['about-movie', 'overlay'],

  mounted() {
    this.getMovies();
  },

  methods: {
    movieAbout(movie) {
      this.$emit('about-movie', movie);
    },

    getMoviesBySearch() {
      this.loading = true;
      this.movies = [];
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=${
            this.apiKey
          }&language=en-US&page=1&query=${encodeURI(this.query)}`
        )
        .then((response) => {
          if (response.data.results.length === 0) {
            this.loading = false;
            this.message = 'No records found.';
          } else {
            this.movies = response.data.results;
            this.loading = false;
            this.query = '';
            this.message = '';
          }
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getMovies() {
      this.searchedMovie = false;
      this.loading = true;
      axios
        .get(
          `https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=${this.apiKey}&page=${this.page}&language=en`
        )
        .then((response) => {
          this.movies = response.data.results;
          this.loading = false;
          this.message = '';
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getMorePopularMovies() {
      this.searchedMovie = false;
      this.loading = true;
      this.page = this.page + 1;

      axios
        .get(
          `https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=${this.apiKey}&page=${this.page}&language=en`
        )
        .then((response) => {
          response.data.results.forEach((data) => {
            this.movies.push(data);
          });
          this.loading = false;
          this.message = '';
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getTopRatedMovies() {
      this.searchedMovie = false;
      this.loading = true;
      this.movies = [];
      axios
        .get(
          `https://api.themoviedb.org/3/movie/top_rated?sort_by=popularity.desc&api_key=${this.apiKey}&language=en-US&page=${this.page}`
        )
        .then((response) => {
          this.movies = response.data.results;
          this.loading = false;
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getMoreTopRatedMovies() {
      this.searchedMovie = false;
      this.loading = true;
      this.page = this.page + 1;

      axios
        .get(
          `https://api.themoviedb.org/3/movie/top_rated?sort_by=popularity.desc&api_key=${this.apiKey}&language=en-US&page=${this.page}`
        )
        .then((response) => {
          response.data.results.forEach((data) => {
            this.movies.push(data);
          });
          this.loading = false;
          this.message = '';
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getUpcomingMovies() {
      this.searchedMovie = false;
      this.loading = true;
      this.movies = [];
      axios
        .get(
          `https://api.themoviedb.org/3/movie/upcoming?api_key=${this.apiKey}&language=en-US&page=${this.page}&region=us`
        )
        .then((response) => {
          this.movies = response.data.results;
          this.loading = false;
          this.message = '';
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getMoreUpcomingMovies() {
      this.searchedMovie = false;
      this.loading = true;
      this.page = this.page + 1;

      axios
        .get(
          `https://api.themoviedb.org/3/movie/upcoming?api_key=${this.apiKey}&language=en-US&page=${this.page}&region=us`
        )
        .then((response) => {
          response.data.results.forEach((data) => {
            this.movies.push(data);
          });

          this.loading = false;
          this.message = '';
        })
        .catch((error) => {
          console.error(error);
        });
    },

    // data about single movie
    aboutMovie(movie) {
      this.$emit('movie-info', movie);
      //console.log(movie);
    },
  },
};
</script>

<style lang="scss" scoped></style>
