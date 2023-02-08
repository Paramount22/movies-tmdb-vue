<template>
  <form @submit.prevent="formSubmitted">
    <input
      class="search-input"
      v-model="searchValue"
      @input="this.$emit('searchedQuery', searchValue)"
      type="text"
      placeholder="Search person"
    />

    <button type="submit">
      <img src="/images/find.svg" alt="Search icon" />
    </button>
  </form>
</template>

<script>
export default {
  name: 'PeopleSearch',

  data() {
    return {
      searchValue: '',
    };
  },

  methods: {
    formSubmitted() {
      if (!this.searchValue) return;
      this.$emit('form-submitted');
      this.$emit('star-search-people');
      this.searchValue = '';
    },
  },
};
</script>

<style lang="scss" scoped></style>
