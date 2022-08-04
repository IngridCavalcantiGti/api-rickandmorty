<!-- eslint-disable prettier/prettier -->
<template>
  <div
    class="shadow-lg m-10 p-2 w-60 bg-green-700 border-2 border-green-200"
    v-for="(character, index) in characters"
    :key="index"
  >
    <img class="w-full" :src="character.image" alt="image" />

    <div class="px-6 py-2">
      <p class="text-white font-bold text--center">{{ character.name }}</p>
      <p class="text-white text-base text--center">{{ character.status }}</p>
      <p class="text-white text-base text--center">{{ character.species }}</p>
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
