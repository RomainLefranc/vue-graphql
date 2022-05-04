<template lang="">
  <div class="mx-auto flex flex-col w-44 bg-white rounded-2xl border shadow-xl shadow-slate-300/60 overflow-hidden mb-3">
    <img class="rounded-t-2xl h-72 w-full object-cover object-center flex-none" :src="character.image" alt="" />
    <div class="flex h-full items-center bg-gray-800">
      <div class="p-5 w-full flex justify-between items-center gap-1">
        <h5 class="text-base font-bold tracking-tight text-gray-900 dark:text-white">{{ character.full }}</h5>
        <button
          v-if="!character.liked"
          type="button"
          v-on:click="like"
          class="text-white bg-gradient-to-r from-cyan-500 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-2.5 py-1 text-center"
        >
          <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M5 4a2 2 0 012-2h6a2 2 0 012 2v14l-5-2.5L5 18V4z"></path></svg>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  props: ["character"],
  name: "characterCard",
  methods: {
    like: function (event) {
      axios
        .post("http://localhost:1337/api/characters/", {
          fullName: this.character.full,
          firstName: this.character.first,
          lastName: this.character.last,
          imageUrl: this.character.image,
        })
        .then(() => {
          this.character.liked = true;
        });
    },
  },
};
</script>
<style lang=""></style>
