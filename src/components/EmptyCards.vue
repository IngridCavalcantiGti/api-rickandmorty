<template>
  <h1 class="text-4xl p-20 text-white">{{ CharactersNotFound }}</h1>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  props: {
    CharactersNotFound: { type: String },
  },
});
</script>