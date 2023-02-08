<template>
  <Transition name="scale">
    <div class="overlay" v-if="overlay" v-cloak>
      <section class="tmdb-data-about fade">
        <img
          class="tmdb-data-poster"
          :src="`${IMG_PATH}${personInfo.profile_path}`"
          alt=""
        />
        <article class="about">
          <header class="tmdb-data-about-header">
            <h2>
              {{ personInfo.name }}
            </h2>
            <div
              class="tmdb-data-close-overlay"
              @click="this.$emit('overlay-close')"
            >
              X
            </div>
          </header>

          <p>
            <span v-if="personInfo.birthday"
              >Birth:
              {{ modifieStringDate(personInfo.birthday) }}
              - {{ personInfo.place_of_birth }}</span
            >
            <span v-if="personInfo.deathday"
              >Dead: {{ modifieStringDate(personInfo.deathday) }}</span
            >
          </p>

          <p class="person-bio">{{ personInfo.biography }}</p>
        </article>
      </section>
    </div>
  </Transition>
</template>

<script>
export default {
  name: 'PersonAbout',

  props: {
    overlay: {
      type: Boolean,
    },
    personInfo: {
      type: Object,
    },
  },

  data() {
    return {
      IMG_PATH: 'https://image.tmdb.org/t/p/w1280',
    };
  },

  methods: {
    modifieStringDate(character) {
      character = character.split('-').reverse();

      const fromIndex = character.indexOf('24');
      //console.log(fromIndex);

      const toIndex = 2;
      const element = character.splice(fromIndex, 1)[0];
      //console.log(element);

      character.splice(toIndex, 0, element);

      character = character.join('.');

      return character;
    },

    calculateAge(string) {
      const date = string.slice(0, 4);

      const year = new Date().getFullYear();

      return year - +date;
    },
  },
};
</script>

<style lang="scss" scoped>
[v-cloak] {
  display: none;
}
.tmdb-data-about {
  padding: 1rem;
  width: 80vw;
  max-height: 70vh;
  background-color: #2c3e50;
  display: flex;
  box-shadow: 0 0 5px white;
  border-radius: 1rem;
  position: relative;
  overflow-y: scroll;

  @media (max-width: 730px) {
    flex-direction: column;
  }

  .tmdb-data-poster {
    @media (max-width: 730px) {
      width: 10rem;
      height: 10rem;
    }
  }

  .about {
    display: flex;
    flex-direction: column;
    font-size: 1.2rem;
    padding: 0.5rem 1rem;

    p {
      margin: 0.3rem 0;
      text-align: justify;

      span {
        font-size: 0.9rem;
        position: relative;
        bottom: 0.7rem;
        display: block;
      }
    }

    .tmdb-data-about-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
  }
}

.tmdb-data-poster {
  width: 15rem;
  height: 20rem;
  border-radius: 1rem;
  object-fit: cover;
}

.tmdb-data-date {
  display: flex;
  p {
    margin-right: 1rem;
  }
}

.about {
  flex: 1;
}

.person-bio {
  padding-bottom: 1rem;
}

.tmdb-data-close-overlay {
  font-size: 2rem;
  font-weight: bold;
  cursor: pointer;

  @media (max-width: 730px) {
    position: absolute;
    right: 0;
    bottom: 11rem;
  }
}

.scale-enter-active,
.scale-leave-active {
  transition: all 0.2s ease-out;
}

.scale-enter-from,
.scale-leave-to {
  opacity: 0;
  transform: scale(0.75);
}
</style>
