<template>
  <div class="bg-gray-800">
    <div class="flex justify-end flex-wrap p-5">
      <Button label="Status Alive" class="m-2" />
      <Button label="Species Human" class="m-2" />
      <Button label="Grouping by status" class="m-2" />
    </div>

    <Search @onInput="onInput" class="mb-5" />
    <div class="flex flex-wrap">
      <Card :characters="characters"></Card>
    </div>
    <div>
      <Pagination
        labelNext="Next"
        labelPrev="Prev"
        class="p-10"
        @onClickNext="next"
        @onClickPrev="prev"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import axios from "axios";
import Card from "@/components/Card.vue";
import Search from "@/components/Search.vue";
import Button from "@/components/Button.vue";
import Pagination from "@/components/Pagination.vue";

export default defineComponent({
  components: { Card, Search, Button, Pagination },
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

    const next = () => {
      console.log("next");
    };

    const prev = () => {
      console.log("prev");
    };

    return { characters, getAll, onInput, next, prev };
  },
});
</script>
