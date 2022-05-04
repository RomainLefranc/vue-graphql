<template lang="">
  <div class="mx-auto mt-3 max-w-xl">
    <guessCharacterCard class="mt-2" v-if="character" :character="character" />
    <form @submit="check">
      <div>
        <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900">Qui est-ce ?</label>
        <input
          type="text"
          v-model="answerInput"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
        />
        <button
          type="submit"
          class="mt-2 text-white bg-gradient-to-r from-cyan-500 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
        >
          Envoyer
        </button>
        {{ message }}
        Score : {{ score }} | Meilleur score : {{ bestScore }}
      </div>
    </form>
  </div>
</template>
<script>
import axios from "axios";
import guessCharacterCard from "../components/guessCharacterCard.vue";

export default {
  components: { guessCharacterCard },
  name: "Guess",
  data: () => ({
    character: null,
    isLoading: true,
    answerInput: "",
    score: 0,
    bestScore: 0,
    message: "",
  }),
  methods: {
    check: function (event) {
      event.preventDefault();
      if (this.answerInput.toLowerCase() === this.character.full.toLowerCase()) {
        this.score = this.score + 1;
        this.answerInput = "";
        this.getRandomCharacter();
      } else {
        this.bestScore = this.score;
        this.score = 0;
        this.answerInput = "";
        this.getRandomCharacter();
      }
    },
    getRandomCharacter: function (event) {
      let rand = Math.random() * 5000;
      rand = Math.floor(rand);
      axios
        .get(`http://localhost:1337/api/graphql/getRandom`)
        .then((response) => {
          this.character = response.data;
        })
        .catch((error) => {
          this.getRandomCharacter();
        })
        .finally(() => {
          this.isLoading = false;
        });
    },
  },
  mounted() {
    this.getRandomCharacter();
  },
};
</script>
<style lang=""></style>
