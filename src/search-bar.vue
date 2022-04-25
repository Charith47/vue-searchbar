<template>
  <div>
    <label for="search-bar"></label>
    <input ref="input" type="text" name="search-bar" @input="debouncedInput" />
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
    };
  },
  created() {
    // add event listner for '/' shortcut
    document.addEventListener("keydown", this.handleDocumentShortcuts);
  },
  methods: {
    enter(e) {
      this.query = e.target.value;
    },
    handleDocumentShortcuts(e) {
      console.log("key pressed", e);
      if (e.key === "/" && !this.hasFocus) {
        e.preventDefault();
        this.$refs.input.focus();
      }
    },
  },
  computed: {
    debouncedInput() {
      return debounce(this.enter, this.delay);
    },
  },
};
</script>

<style scoped>
#widget {
  background: crimson;
  width: fit-content;
  height: fit-content;
}
</style>