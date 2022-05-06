<template lang="">
  <div
    class="mx-auto flex flex-col w-44 bg-white rounded-2xl overflow-hidden mb-3"
  >
    <img
      class="rounded-t-2xl h-72 w-full object-cover object-center flex-none"
      :src="character.image"
      alt=""
    />
    <div class="flex h-full items-center bg-gray-800">
      <div class="p-5 w-full flex justify-between items-center gap-1">
        <h5
          class="text-base font-bold tracking-tight text-gray-900 dark:text-white"
        >
          {{ character.full }}
        </h5>
        <button
          v-if="character.liked"
          type="button"
          v-on:click="dislike"
          class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-2.5 py-1 text-center"
        >
          <svg
            class="w-6 h-6"
            fill="currentColor"
            viewBox="0 0 20 20"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              fill-rule="evenodd"
              d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
              clip-rule="evenodd"
            ></path>
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  props: ["character"],
  name: "likedCharacterCard",

  methods: {
    dislike: function (event) {
      axios
        .delete(
          `http://localhost:1337/api/characters/${encodeURIComponent(
            this.character.id
          )}`
        )
        .then(() => {
          this.$emit("suppression", this.character.id);
        });
    },
  },
};
</script>
<style lang=""></style>
