<script>
import Vue from 'vue';
import SearchBar from '@/search-bar.vue';
import '@/search-bar.css'
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
