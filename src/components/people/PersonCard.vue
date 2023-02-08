<template>
  <div
    class="tmdb-data-card"
    @click="getPersonInfo(person.id), this.$emit('overlay-open')"
  >
    <img
      class="tmdb-data-poster"
      :src="`${IMG_PATH}${person.profile_path}`"
      :alt="person.name"
    />

    <h4 class="tmdb-data-title">{{ person.name }}</h4>

    <div class="tmdb-data-department">
      {{ person.known_for_department }}
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'PersonCard',

  props: {
    person: {
      type: Object,
    },
  },

  data() {
    return {
      IMG_PATH: 'https://image.tmdb.org/t/p/w1280',
      apiKey: '8335b966aa0001f618384081f205b83d',
      overlay: false,
    };
  },

  methods: {
    getPersonInfo(personId) {
      axios
        .get(
          `https://api.themoviedb.org/3/person/${personId}?api_key=${this.apiKey}&language=en-US`
        )
        .then((response) => {
          //console.log(new Date() - +response.data.birthday.slice(0, 4));
          this.$emit('person-data', response.data);
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style lang="scss" scoped></style>
