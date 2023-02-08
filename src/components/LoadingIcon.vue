<template>
  <div v-if="loading" class="loading">
    <img src="/images/loading-light.svg" alt="loading" />
  </div>
</template>

<script>
export default {
  name: 'LoadingIcon',

  props: {
    loading: {
      type: Boolean,
    },
  },
};
</script>

<style lang="scss" scoped></style>
