<script setup>
import { ref, onMounted } from 'vue';
import CardIndex from "@/components/utility/CardIndex.vue";
import { allPokemonData } from "@/services/ApiService.vue";

console.log('pokeindex', allPokemonData);

let itemsToDisplay = ref(10);
const itemsPerLoad = 10;

onMounted(() => {
  window.addEventListener('scroll', () => {
    if ((window.innerHeight + window.scrollY) >= document.body.offsetHeight) {
      itemsToDisplay.value += itemsPerLoad;
    }
  });
});
</script>

<template>
  <div id="pokemonIndexArea" class="index-wrapper">
    <CardIndex v-for="(pokemon, index) in (allPokemonData[0] ? allPokemonData[0].slice(0, itemsToDisplay.value) : [])" :key="index" :pokemon="pokemon" />
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
}
</style>
