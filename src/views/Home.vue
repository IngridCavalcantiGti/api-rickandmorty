<template>
  <div class="bg-gray-400">
    <Search @onInput="onInput" />
    <div class="flex flex-wrap">
      <Card :characters="characters" class="border-gray-400 border-4"></Card>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import axios from "axios";
import Card from "@/components/Card.vue";
import Search from "@/components/Search.vue";

export default defineComponent({
  components: { Card, Search },
  setup() {
    const characters = ref(null);

    onMounted(() => {
      getAll();
    });

    const getAll = () => {
      axios
        .get(`https://rickandmortyapi.com/api/character`)
        .then((response) => {
          characters.value = response.data.results;
        })
        .catch((error) => console.log(error));
    };

    const onInput = (value: string) => {
      console.log(value);
    };

    return { characters, getAll, onInput };
  },
});
</script>
