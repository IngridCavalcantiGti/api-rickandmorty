<template>
  <div>
    <h2 v-if="title" class="flex justify-center flex-wrap">
      {{ title }}
    </h2>
    <div class="flex justify-center flex-wrap">
      <div
        class="shadow-lg m-4 p-2 w-60 bg-green-700 border-2 border-green-200"
        v-for="(character, index) in characters"
        :key="index"
      >
        <img class="w-full" :src="character.image" alt="image" />

        <div class="px-6 py-2 text--center h-20">
          <p class="text-white font-bold mb-5x">{{ character.name }}</p>
        </div>
        <div class="text--center">
          <p class="text-white text-base bg-gray-400 border mb-2 rounded-full">
            {{ character.status }}
          </p>
          <p
            class="
              text-white text-base text--center
              bg-gray-400
              border
              rounded-full
            "
          >
            {{ character.species }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    characters: { type: Array },
    title: { type: String },
  },
});
</script>
