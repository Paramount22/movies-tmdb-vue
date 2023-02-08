<template>
  <div class="filter">
    <a href="#" @click.prevent="this.$emit('get-movies')">Popular</a>
    <a href="#" @click.prevent="this.$emit('get-top-rated-movies')"
      >Top Rated</a
    >
    <a href="#" @click.prevent="this.$emit('get-upcoming-movies')">Upcoming</a>
  </div>
</template>

<script>
export default {
  name: 'MoviesFilter',

  emits: ['get-movies', 'get-top-rated-movies', 'get-upcoming-movies'],

  mounted() {
    this.addRemvoveActiveClass();
  },

  methods: {
    addRemvoveActiveClass() {
      const filterLinks = document.querySelectorAll('.filter a');
      filterLinks[0].classList.add('active');
      filterLinks.forEach((link, index) => {
        link.addEventListener('click', () => {
          if (index === 0) {
            link.classList.add('active');
            link.nextElementSibling.classList.remove('active');
            link.nextElementSibling.nextElementSibling.classList.remove(
              'active'
            );
          }

          if (index === 1) {
            link.classList.add('active');
            link.nextElementSibling.classList.remove('active');
            link.previousElementSibling.classList.remove('active');
          }

          if (index === 2) {
            link.classList.add('active');
            link.previousElementSibling.classList.remove('active');
            link.previousElementSibling.previousElementSibling.classList.remove(
              'active'
            );
          }
        });
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
