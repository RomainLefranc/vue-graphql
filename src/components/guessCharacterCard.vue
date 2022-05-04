<template lang="">
  <div class="mx-auto flex flex-col w-44 bg-white rounded-2xl shadow-xl shadow-slate-300/60 overflow-hidden mb-3">
    <img class="rounded-2xl h-72 w-full object-cover object-center flex-none" :src="character.image" alt="" />
  </div>
</template>
<script>
export default {
  props: ["character"],
  name: "characterCard",
};
</script>
<style lang=""></style>
