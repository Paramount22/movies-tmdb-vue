<template>
  <TransitionGroup tag="div" name="list" class="tmdb-data">
    <PersonCard
      v-for="person in people"
      :key="person.id"
      :person="person"
      @overlay-open="this.$emit('overlay-open')"
      @person-data="getPersonData($event)"
    />
  </TransitionGroup>
</template>

<script>
import PersonCard from './PersonCard.vue';
export default {
  name: 'PeopleList',

  components: {
    PersonCard,
  },

  props: {
    people: {
      type: Array,
    },
  },

  methods: {
    getPersonData(data) {
      this.$emit('get-person-data', data);
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
