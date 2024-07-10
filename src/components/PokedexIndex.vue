<script setup>
import { ref, onMounted, watch, inject } from 'vue';
import CardIndex from "@/components/utility/CardIndex.vue";
import { allPokemonData } from "@/services/ApiService.vue";
import CardDetail from "@/components/utility/CardDetail.vue";

console.log('showApi for interested People', allPokemonData);

const filterValue = inject('filterValue');
let itemsToDisplay = ref(10);
const itemsPerLoad = 10;
let openDetail = ref(false);
const selectedPokemon = ref(null);
const filteredPokemon = ref([]);
const filterState = ref('initial');

onMounted(() => {
  window.addEventListener('scroll', () => {
    if ((window.innerHeight + window.scrollY) >= document.body.offsetHeight) {
      itemsToDisplay.value += itemsPerLoad;
    }
  });
});

watch(filterValue, (newValue) => {

  if (newValue === '') {
    filterState.value = 'all';
  } else {
    filterState.value = 'filtered';
  }

  switch (filterState.value) {
    case 'initial':
      filteredPokemon.value = allPokemonData[0];
      break;
    case 'filtered':
      filteredPokemon.value = allPokemonData[0].filter(pokemon => pokemon.name.toLowerCase().includes(newValue.toLowerCase()));
      break;
    case 'all':
      filteredPokemon.value = allPokemonData[0];
      break;
  }
});

const openPokemon = (pokemon) => {
  selectedPokemon.value = pokemon;
  openDetail.value = true;
};

const closeDetail = () => {
  openDetail.value = false;
  selectedPokemon.value = null;
};

</script>

<template>
  <div id="pokemonIndexArea" class="index-wrapper">
    <div v-if="!filterValue" class="filter-wrapper">
      <card-index v-for="(pokemon, index) in (allPokemonData[0] ? allPokemonData[0].slice(0, itemsToDisplay.value) : [])" :key="index" :pokemon="pokemon"  @open-pokemon="openPokemon(pokemon)" />
    </div>
    <div v-if="filterValue" class="filter-wrapper">
      <card-index v-for="(pokemon, index) in filteredPokemon.slice(0, itemsToDisplay.value)" :key="index" :pokemon="pokemon" @open-pokemon="openPokemon(pokemon)" />
    </div>

    <card-detail :visible="openDetail" :pokemon="selectedPokemon" class="detail-wrapper" @close="closeDetail"></card-detail>
  </div>
</template>

<style scoped lang="scss">
.index-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 1rem;
  width: 100%;
  height: 100%;
  position: relative;
  .detail-wrapper{
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    display: flex;
    width: 100%;
    height: 100%;
    z-index: 100;
  }
}

.filter-wrapper {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  height: 100%;
}
</style>
