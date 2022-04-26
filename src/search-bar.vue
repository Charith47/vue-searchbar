<template>
  <div>
    <label for="search-bar"></label>
    <input
      class="
        bg-gray-200
        appearance-none
        border-2 border-gray-200
        rounded
        w-full
        py-2
        px-4
        text-gray-700
        leading-tight
        focus:outline-none focus:bg-white focus:border-blue-500
      "
      ref="input"
      type="text"
      name="search-bar"
      @input="debouncedInput"
      @focus="hasFocus = true"
      @blur="hasFocus = false"
    />
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
      hasFocus: false,
    };
  },
  created() {
    // add event listner for shortcuts
    // '/' for focusing on searchbar
    // ESC to clear searchbar and unfocus
    document.addEventListener("keydown", this.handleDocumentShortcuts);
  },
  methods: {
    enter(e) {
      this.query = e.target.value;
      this.$emit("search", this.query);
    },
    handleDocumentShortcuts(e) {
      if (e.key === "/" && !this.hasFocus) {
        e.preventDefault();
        this.$refs.input.focus();
      } else if (e.key === "Escape" && this.hasFocus) {
        e.preventDefault();
        this.$nextTick(() => {
          this.$refs.input.value = "";
          this.$refs.input.blur();
        });
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