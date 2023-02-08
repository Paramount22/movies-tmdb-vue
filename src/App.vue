<template>
  <header>
    <div class="wrapper">
      <RouterLink to="/"
        ><img src="/images/Logo.svg" width="180" alt="tmdb logo"
      /></RouterLink>
      <nav>
        <RouterLink to="/">Movies</RouterLink>
        <RouterLink to="/people">People</RouterLink>
        <RouterLink to="/series">Series</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />

  <footer>
    <RouterLink to="/"
      ><img src="/images/Logo.svg" width="180" alt="tmdb logo"
    /></RouterLink>
  </footer>
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router';
</script>

<style lang="scss" scoped>
header {
  background-color: darken(#2c3e50, 10%);
  padding: 1rem 0;

  nav {
    margin-bottom: 0.5rem;
    margin-left: 1rem;
  }

  a {
    margin-left: 1rem;
    font-size: large;

    &:first-child {
      margin-left: 0;
    }
  }

  .wrapper {
    width: 100%;
    padding: 0 2rem;
    display: flex;
    align-items: center;

    @media (max-width: 432px) {
      flex-direction: column;
    }
  }

  .router-link-active {
    font-weight: 600;
  }
}

footer {
  background-color: darken(#2c3e50, 10%);
  padding: 1rem 2rem;
  margin-top: 1rem;
}
</style>
