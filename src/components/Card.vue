<template>
  <div
    class="shadow-lg m-10 h-50 w-40"
    v-for="(character, index) in characters"
    :key="index"
  >
    <img class="w-full" :src="character.image" alt="image" />

    <div class="px-6 py-4">
      <p class="text-gray-700 font-bold">{{ character.name }}</p>
      <p class="text-gray-700 text-base">{{ character.status }}</p>
      <p class="text-gray-700 text-base">{{ character.species }}</p>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    characters: { type: Object },
  },
});
</script>