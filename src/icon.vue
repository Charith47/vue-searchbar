<template>
  <div class="absolute py-2 px-2">
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-6 w-6 text-indigo-400 dark:text-indigo-500 fill-current"
      viewBox="0 0 24 24"
      stroke-width="2"
    >
      <path
        fill-rule="evenodd"
        stroke-linecap="round"
        stroke-linejoin="round"
        :d="path"
      ></path>
    </svg>
  </div>
</template>

<script>
export default {
  props: {
    size: {
      type: Number,
      default: 24,
    },
    color: {
      type: String,
      default: "black",
    },
    path: {
      type: String,
      required: true,
    },
  },
};
</script>
