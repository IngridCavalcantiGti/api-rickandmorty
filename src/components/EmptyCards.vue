<template>
  <h1 class="text-4xl p-20 text-center text-green-400">
    {{ CharactersNotFound }}

    <div class="text-9xl">
      <img class="w-40 absolute" src="@/assets/404.png" alt="image" />
      <span class="text-9xl">4 4</span>
    </div>
  </h1>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  props: {
    CharactersNotFound: { type: String },
  },
});
</script>