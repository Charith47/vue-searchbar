<template>
  <div class="px-4 py-4 dark:bg-gray-900">
    <icon :path="icons.mdiMagnify"></icon>
    <label for="search-bar"></label>
    <input
      class="
        appearance-none
        rounded
        leading-tight
        py-2
        pr-4
        pl-8
        bg-gray-200
        dark:bg-gray-700
        text-gray-700
        dark:text-gray-100
        focus:outline-none focus:bg-white
        border-2 border-gray-200
        dark:border-gray-700
        focus:border-indigo-400
        dark:focus:border-indigo-500
      "
      ref="input"
      type="text"
      name="search-bar"
      :placeholder="placeholder ? placeholder : 'Search..'"
      @input="debouncedInput"
      @focus="hasFocus = true"
      @blur="hasFocus = false"
    />
    <p class="text-gray-700 dark:text-gray-200">{{ query }}</p>
  </div>
</template>

<script>
import debounce from "lodash.debounce";
import { mdiMagnify } from "@mdi/js";
import icon from "@/components/icon.vue";

export default /*#__PURE__*/ {
  props: {
    delay: {
      type: Number,
      default: 350,
    },
    placeholder: {
      type: String,
      default: "Search",
    },
  },
  name: "SearchBar",
  components: {
    icon,
  },
  data() {
    return {
      query: "",
      hasFocus: false,
      icons: {
        mdiMagnify,
      },
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

      // validate input
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

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>