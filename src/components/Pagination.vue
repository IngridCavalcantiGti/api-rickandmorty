<!-- eslint-disable prettier/prettier -->
<template>
  <div class="flex justify-center">
    <button
      @click="() => $emit('onClickPrev')"
      type="button"
      class="
        text-white
        font-medium
        text-xs
        leading-tight
        uppercase
        rounded
        shadow-md
        mr-5
        hover:text-green-400 hover:shadow-lg
      "
    >
      <div class="flex flex-auto">
        <svg
          class="w-6 h-6"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M11 19l-7-7 7-7m8 14l-7-7 7-7"
          ></path>
        </svg>
        <span class="mt-1">{{ labelPrev }}</span>
      </div>
    </button>

    <button
      @click="() => $emit('onClickNext')"
      type="button"
      class="
        text-white
        font-medium
        text-xs
        leading-tight
        uppercase
        rounded
        shadow-md
        hover:text-green-400 hover:shadow-lg
      "
    >
      <div class="flex">
        <span class="mt-1">{{ labelNext }}</span>
        <svg
          class="w-6 h-6"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M13 5l7 7-7 7M5 5l7 7-7 7"
          ></path>
        </svg>
      </div>
    </button>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    labelNext: { type: String },
    labelPrev: { type: String },
  },
});
</script>
