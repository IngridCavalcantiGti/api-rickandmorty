<template>
  <div class="bg-gray-800 min-h-screen">
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
        @keyup.enter="filter"
      />
      <div></div>
    </div>

    <div class="flex flex-wrap justify-center">
      <Card :characters="characters" v-if="showCards && !grouped"></Card>
      <template v-else-if="showCards">
        <Card :characters="dead" title="Dead" class="text-white"></Card>
        <Card :characters="alive" title="Alive" class="text-white"></Card>
        <Card :characters="unknown" title="Unknown" class="text-white"></Card>
      </template>

      <EmptyCards
        :CharactersNotFound="CharactersNotFoundTitle"
        v-if="charactersNotFound"
      ></EmptyCards>
    </div>

    <div v-if="showPagination">
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
import { defineComponent, ref, onMounted, watch, computed } from "vue";
import axios from "axios";
import Card from "@/components/Card.vue";
import Search from "@/components/Search.vue";
import Button from "@/components/Button.vue";
import Pagination from "@/components/Pagination.vue";
import EmptyCards from "@/components/EmptyCards.vue";

export default defineComponent({
  components: { Card, Search, Button, Pagination, EmptyCards },
  setup() {
    const characters = ref([]);
    const search = ref("");
    const info = ref({ next: "", prev: "" });
    const apiUrl = "https://rickandmortyapi.com/api/character/";
    const charactersNotFound = ref(false);
    const showCards = ref(true);
    const CharactersNotFoundTitle = ref("");
    const showPagination = ref(true);

    onMounted(() => {
      getAll(apiUrl);
    });

    const getAll = (url: string) => {
      return axios
        .get(url)

        .then((response) => {
          characters.value = response.data.results;
          info.value = response.data.info;
        })
        .catch(() => {
          CharactersNotFoundTitle.value = "Not found";
          charactersNotFound.value = true;
          showCards.value = false;
          showPagination.value = false;
        });
    };

    type Character = {
      name: string;
      status: string;
      image: string;
      species: string;
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
      getAll(apiUrl + "?species=human").then(() => {
        characters.value = characters.value.filter((character: Character) => {
          return character.species === "Human";
        });
      });
    };

    const dead = computed(() => {
      return characters.value.filter(
        (character: Character) => character.status === "Dead"
      );
    });

    const unknown = computed(() => {
      return characters.value.filter(
        (character: Character) => character.status === "unknown"
      );
    });

    const alive = computed(() => {
      return characters.value.filter(
        (character: Character) => character.status === "Alive"
      );
    });

    const grouped = ref(false);

    const clickGrouping = () => {
      grouped.value = !grouped.value;
    };

    watch(search, () => {
      if (search.value.length < 1) {
        showCards.value = true;
        charactersNotFound.value = false;
        showPagination.value = true;
        getAll(apiUrl);
      }
    });

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
      charactersNotFound,
      showCards,
      CharactersNotFoundTitle,
      showPagination,
      alive,
      unknown,
      dead,
      grouped,
    };
  },
});
</script>
