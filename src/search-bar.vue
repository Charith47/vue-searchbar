<template>
  <div class="widget">
    <input v-model="query" type="text">
  </div>
</template>

<script>

export default /*#__PURE__*/{
  name: 'SearchBar',
  data() {
    return {
      query: '',
    };
  },
};
</script>

<style scoped>
</style>
