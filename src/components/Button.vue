<template>
  <div>
    <button
      @click="() => $emit('onClick')"
      type="button"
      class="
        inline-block
        px-6
        py-3
        bg-green-700
        text-white
        font-medium
        text-xs
        leading-tight
        uppercase
        rounded
        shadow-md
        hover:bg-green-800 hover:shadow-lg
        focus:bg-green-800 focus:shadow-lg focus:outline-none focus:ring-0
        active:bg-green-800 active:shadow-lg
      "
    >
      {{ label }}
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  props: {
    label: {
      type: String,
    },
  },
});
</script>
