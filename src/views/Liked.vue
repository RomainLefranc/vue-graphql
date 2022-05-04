<template lang="">
  <div class="mx-auto mt-3 max-w-6xl">
    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6">
      <likedCharacterCard @suppression="logChange" v-for="character in characters" :key="character" :character="character" />
    </div>
  </div>
</template>
<script>
import axios from "axios";
import likedCharacterCard from "../components/likedCharacterCard.vue";
export default {
  name: "Liked",
  data: () => ({
    characters: [],
    isLoading: true,
  }),
  components: { likedCharacterCard },
  mounted() {
    this.isLoading = true;
    axios
      .get("http://localhost:1337/api/characters")
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
  methods: {
    logChange: function (event) {
      this.characters = this.characters.filter((character) => character.fullName != event);
    },
  },
};
</script>
<style lang=""></style>
