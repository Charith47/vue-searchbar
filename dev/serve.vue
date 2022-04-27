<script>
import Vue from "vue";
import SearchBar from "@/search-bar.vue";

export default Vue.extend({
  name: "ServeDev",
  components: {
    SearchBar,
  },
  data() {
    return {
      isDark: true,
    };
  },
});
</script>

<template>
  <div :class="isDark ? 'dark' : ''" id="app">
    <button @click="isDark = !isDark"> Toggle mode</button>
    <search-bar />
  </div>
</template>
