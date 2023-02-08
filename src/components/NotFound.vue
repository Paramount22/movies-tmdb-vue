<template>
  <h2 v-if="message">{{ message }}</h2>
</template>

<script>
export default {
  name: 'NotFound',

  props: {
    message: {
      type: String,
    },
  },
};
</script>

<style lang="scss" scoped>
h2 {
  text-align: center;
  font-size: 2rem;
}
</style>
