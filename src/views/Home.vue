<template>
  <div class="bg-gray-800">
    <div class="flex justify-center p-2">
      <img src="@/assets/Rick-And-Morty-Logo.png" class="w-1/4" />
    </div>
    <div class="flex justify-center flex-wrap gap-4 pt-5">
      <Button label="Status Alive" @onClick="clickAlive" />
      <Button label="Species Human" @onClick="clickHuman" />
      <Button
        label="Grouping by status"
        class="mr-10"
        @onClick="clickGrouping"
      />
      <Search
        @onInput="onInput"
        class="mb-5"
        :value="search"
        @onFilter="filter"
      />

      <div></div>
    </div>

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
    const characters = ref([]);
    const search = ref("");
    const info = ref({ next: "", prev: "" });
    const apiUrl = "https://rickandmortyapi.com/api/character/";
    onMounted(() => {
      getAll(apiUrl);
    });

    const getAll = (url: string) => {
      axios
        .get(url)

        .then((response) => {
          characters.value = response.data.results;
          info.value = response.data.info;
        })
        .catch((error) => console.log(error));
    };

    const onInput = (value: string) => {
      search.value = value.toLowerCase();
    };

    const filter = () => {
      const statusList = ["alive", "dead", "unknown"];
      if (statusList.includes(search.value)) {
        getAll(`${apiUrl}?status=${search.value}`);
        return;
      }
      getAll(`${apiUrl}?name=${search.value}`);
    };

    const next = () => {
      if (info.value.next) {
        getAll(info.value.next);
      }
    };

    const prev = () => {
      if (info.value.prev) {
        getAll(info.value.prev);
      }
    };

    const clickAlive = () => {
      getAll(apiUrl + "?status=alive");
    };

    const clickHuman = () => {
      getAll(apiUrl + "?species=human");
    };

    const clickGrouping = () => {
      console.log("clickGrouping");
    };

    return {
      characters,
      getAll,
      onInput,
      next,
      prev,
      clickAlive,
      clickHuman,
      clickGrouping,
      search,
      filter,
    };
  },
});
</script>
