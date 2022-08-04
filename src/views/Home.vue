<template>
  <div class="home">
    <div class="flex flex-wrap">
      <Card :characters="characters" class="border-gray-400 border-4"></Card>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import axios from "axios";
import Card from "@/components/Card.vue";

export default defineComponent({
  components: { Card },
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

    return { characters, getAll };
  },
});
</script>
