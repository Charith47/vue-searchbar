<script>
import Vue from 'vue';
import SearchBar from '@/search-bar.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    SearchBar
  }
});
</script>

<template>
  <div id="app">
    <search-bar />
  </div>
</template>
