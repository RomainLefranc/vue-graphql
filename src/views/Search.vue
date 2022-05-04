<template lang="">
  <div class="mx-auto max-w-6xl mt-3">
    <form @submit="search">
      <label for="search" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-gray-300">Your Email</label>
      <div class="relative">
        <input
          type="search"
          id="search"
          class="block w-full p-4 text-sm text-gray-900 border border-gray-300 rounded-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="Search"
          v-model="searchInput"
          required
        />
        <button
          type="submit"
          class="text-white absolute right-2.5 bottom-3 bg-gradient-to-r from-cyan-500 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-4 py-1 text-center inline-flex items-center"
        >
          <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd"></path>
          </svg>
        </button>
      </div>
    </form>
    <div class="mt-3 grid grid-cols-6"><characterCard v-for="character in characters" :key="character" :character="character" /></div>
  </div>
</template>
<script>
import axios from "axios";
import characterCard from "../components/characterCard.vue";

export default {
  components: { characterCard },
  name: "Search",
  data: () => ({
    characters: [],
    isLoading: false,
    searchInput: "",
  }),
  methods: {
    search: function (event) {
      event.preventDefault();
      this.isLoading = true;
      axios
        .get(`http://localhost:1337/api/graphql/getByAnime/${encodeURIComponent(this.searchInput)}`)
        .then((response) => {
          this.characters = response.data;
        })
        .catch((error) => {
          console.log(error);
        })
        .finally(() => {
          this.isLoading = false;
        });
    },
  },
};
</script>
<style lang=""></style>
