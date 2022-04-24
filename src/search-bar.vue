<template>
  <div class="widget">
    <label for="search-bar"></label>
    <input type="text" name="search-bar" @input="debouncedInput" />
    <p>{{ query }}</p>
  </div>
</template>

<script>
import debounce from "lodash.debounce";

export default /*#__PURE__*/ {
  props: {
    delay: {
      type: Number,
      default: 350,
    },
  },
  name: "SearchBar",
  data() {
    return {
      query: "",
      results: [],
    };
  },
  methods: {
    enter(e) {
      this.query = e.target.value;
      // call api
    },
  },
  computed: {
    debouncedInput() {
      return debounce(this.enter, this.delay);
    },
  },
};
</script>