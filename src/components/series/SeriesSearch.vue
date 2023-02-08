<template>
  <form @submit.prevent="formSubmitted">
    <input
      class="search-input"
      v-model="searchValue"
      @input="this.$emit('searched-query', searchValue)"
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
  name: 'SeriesSearch',

  data() {
    return {
      searchValue: '',
    };
  },

  methods: {
    formSubmitted() {
      if (!this.searchValue) return;
      this.$emit('form-submitted');
      this.$emit('star-search-series');
      this.searchValue = '';
    },
  },
};
</script>

<style lang="scss" scoped></style>
