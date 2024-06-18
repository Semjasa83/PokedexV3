<script setup>
import CardIndex from "@/components/utility/CardIndex.vue";
import { allPokemon } from "@/services/ApiService.vue";

console.log('pokeindex', allPokemon);

</script>

<template>
  <div class="index-wrapper">
    <CardIndex v-for="(pokemon, index) in allPokemon.value" :key="index" :pokemon="pokemon" />
  </div>
</template>

<style scoped>
.index-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 1rem;
  width: 100%;
  background-color: hsl(0, 0%, 40%);
}
</style>