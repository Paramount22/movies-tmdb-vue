<template>
  <main>
    <LoadingIcon :loading="loading" />

    <div class="tmdb-data-filter">
      <div class="filter">
        <a href="#" @click.prevent="getTvShows">Series</a>
      </div>
      <SeriesSearch
        @searched-query="query = $event"
        @form-submitted="getSeriesBySearch"
        @star-search-series="
          (visibilityBtn = false), (visibilityBtnSearch = true)
        "
      />
    </div>

    <NotFound :message="message" />

    <SeriesList
      :tv-shows="tvShows"
      @tv-show-info="seriesInfo = $event"
      @overlay-open="overlay = true"
    />

    <SeriesMore
      @more-series="getMoreTvShows"
      @more-searched-series="getMoreSeriesBySearch"
      :total-results="totalResults"
      :tv-shows="tvShows"
      :visibility-btn="visibilityBtn"
      :visibility-btn-search="visibilityBtnSearch"
    />
  </main>

  <SeriesAbout
    :seriesInfo="seriesInfo"
    :overlay="overlay"
    @overlay-close="overlay = false"
  />
</template>

<script>
import axios from 'axios';
import SeriesSearch from '../components/series/SeriesSearch.vue';
import SeriesList from '../components/series/SeriesList.vue';
import SeriesMore from '../components/series/SeriesMore.vue';
import SeriesAbout from '../components/series/SeriesAbout.vue';
import LoadingIcon from '../components/LoadingIcon.vue';
import NotFound from '../components/NotFound.vue';

export default {
  components: {
    LoadingIcon,
    SeriesSearch,
    SeriesList,
    SeriesMore,
    SeriesAbout,
    NotFound,
  },

  data() {
    return {
      tvShows: [],
      seriesInfo: {},
      apiKey: '8335b966aa0001f618384081f205b83d',
      loading: false,
      page: 1,
      overlay: false,
      query: '',
      message: '',
      totalResults: null,
      visibilityBtn: true,
      visibilityBtnSearch: false,
    };
  },

  mounted() {
    this.getTvShows();
  },

  methods: {
    getTvShows() {
      this.message = '';
      this.loading = true;
      axios
        .get(
          `https://api.themoviedb.org/3/tv/popular?api_key=${this.apiKey}&language=en-US&page=${this.page}`
        )
        .then((response) => {
          this.tvShows = response.data.results;
          this.loading = false;
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getMoreTvShows() {
      this.loading = true;
      this.page++;
      this.message = '';
      axios
        .get(
          `https://api.themoviedb.org/3/tv/popular?api_key=${this.apiKey}&language=en-US&page=${this.page}`
        )
        .then((response) => {
          response.data.results.forEach((data) => {
            this.tvShows.push(data);
          });
          this.loading = false;
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getSeriesBySearch() {
      this.loading = true;
      this.tvShows = [];
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=${
            this.apiKey
          }&query=${encodeURI(this.query)}&language=en-US&page=${
            this.page
          }&include_adult=false`
        )
        .then((response) => {
          this.totalResults = response.data.total_results;

          if (response.data.results.length === 0) {
            this.loading = false;
            this.message = 'No records found.';
          } else {
            this.tvShows = response.data.results;
            this.loading = false;
            this.message = '';
          }
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getMoreSeriesBySearch() {
      this.loading = true;
      this.page++;
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=${
            this.apiKey
          }&query=${encodeURI(this.query)}&language=en-US&page=${
            this.page
          }&include_adult=false`
        )
        .then((response) => {
          //console.log(response.data.results);
          response.data.results.forEach((data) => {
            this.tvShows.push(data);
          });
          this.loading = false;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style lang="scss" scoped></style>
