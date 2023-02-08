<template>
  <main>
    <LoadingIcon :loading="loading" />
    <div class="tmdb-data-filter">
      <div class="filter">
        <a href="#" @click.prevent="getPeople">People</a>
      </div>
      <PeopleSearch
        @searchedQuery="query = $event"
        @form-submitted="getPersonBySearch"
        @star-search-people="
          (visibilityBtn = false), (visibilityBtnSearch = true)
        "
      />
    </div>
    <NotFound :message="message" />
    <PeopleList
      :people="people"
      @overlay-open="overlay = true"
      @get-person-data="personInfo = $event"
    />
    <PeopleMore
      :total-results="totalResults"
      :people="people"
      @more-people="getMorePeople"
      @more-searched-people="getMorePersonBySearch"
      :visibility-btn="visibilityBtn"
      :visibility-btn-search="visibilityBtnSearch"
    />
  </main>

  <PersonAbout
    :person-info="personInfo"
    :overlay="overlay"
    @overlay-close="overlay = false"
    :total-results="totalResults"
  />
</template>

<script>
import axios from 'axios';
import PeopleList from '../components/people/PeopleList.vue';
import LoadingIcon from '../components/LoadingIcon.vue';
import PeopleMore from '../components/people/PeopleMore.vue';
import PeopleSearch from '../components/people/PeopleSearch.vue';
import PersonAbout from '../components/people/PersonAbout.vue';
import NotFound from '../components/NotFound.vue';

export default {
  components: {
    PeopleList,
    LoadingIcon,
    PeopleMore,
    PeopleSearch,
    NotFound,
    PersonAbout,
  },

  data() {
    return {
      people: [],
      apiKey: '8335b966aa0001f618384081f205b83d',
      page: 1,
      loading: false,
      query: '',
      message: '',
      totalResults: null,
      overlay: false,
      personInfo: {},
      visibilityBtn: true,
      visibilityBtnSearch: false,
    };
  },

  mounted() {
    this.getPeople();
  },

  methods: {
    getPeople() {
      this.loading = true;
      axios
        .get(
          `https://api.themoviedb.org/3/person/popular?api_key=${this.apiKey}&language=en-US&page=${this.page}`
        )
        .then((response) => {
          this.people = response.data.results;
          this.loading = false;
          this.message = '';
          this.visibilityBtn = true;
          this.visibilityBtnSearch = false;
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getMorePeople() {
      this.loading = true;
      this.page++;
      axios
        .get(
          `https://api.themoviedb.org/3/person/popular?api_key=${this.apiKey}&language=en-US&page=${this.page}`
        )
        .then((response) => {
          response.data.results.forEach((data) => {
            this.people.push(data);
          });
          this.loading = false;
          this.message = '';
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getPersonBySearch() {
      this.loading = true;
      this.people = [];
      axios
        .get(
          `https://api.themoviedb.org/3/search/person?api_key=${
            this.apiKey
          }&query=${encodeURI(this.query)}&language=en-US&page=${
            this.page
          }&include_adult=false`
        )
        .then((response) => {
          this.totalResults = response.data.total_results;
          //console.log(this.totalResults);

          if (response.data.results.length === 0) {
            this.loading = false;
            this.message = 'No records found.';
          } else {
            this.people = response.data.results;
            this.loading = false;
            this.message = '';
          }
        })
        .catch((error) => {
          console.error(error);
        });
    },

    getMorePersonBySearch() {
      this.loading = true;
      this.page++;
      axios
        .get(
          `https://api.themoviedb.org/3/search/person?api_key=${
            this.apiKey
          }&query=${encodeURI(this.query)}&language=en-US&page=${
            this.page
          }&include_adult=false`
        )
        .then((response) => {
          //console.log(response.data.results);
          response.data.results.forEach((data) => {
            this.people.push(data);
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
