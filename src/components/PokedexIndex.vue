<script setup>
import CardIndex from "@/components/utility/CardIndex.vue";
import { allPokemon } from "@/services/ApiService.vue";

console.log(allPokemon);
</script>

<template>
  <div class="index-wrapper">
    <CardIndex />
  </div>
</template>

<style scoped>
.index-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1rem;
  width: 100%;
  height: 100%;
  background-color: hsl(0, 0%, 40%);
}
</style>