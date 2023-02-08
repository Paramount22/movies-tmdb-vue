<template>
  <div class="more-data" v-if="people.length">
    <button
      class="more"
      v-show="visibilityBtn"
      @click.prevent="this.$emit('more-people')"
    >
      More
    </button>
  </div>

  <div class="more-data" v-if="people.length">
    <button
      class="more"
      v-show="visibilityBtnSearch && people.length != totalResults"
      @click.prevent="this.$emit('more-searched-people')"
    >
      More
    </button>
  </div>
</template>

<script>
export default {
  name: 'PeopleMore',

  emits: ['more-people', 'more-searched-people'],

  props: {
    people: {
      type: Array,
    },
    totalResults: {
      type: Number,
    },

    visibilityBtn: {
      type: Boolean,
    },
    visibilityBtnSearch: {
      type: Boolean,
    },
  },
};
</script>

<style lang="scss" scoped></style>
