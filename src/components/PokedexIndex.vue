<script setup>
import {ref, onMounted, watch, inject, onUnmounted, nextTick} from 'vue';
import CardIndex from "@/components/utility/CardIndex.vue";
import {allPokemonData} from "@/services/ApiService.vue";
import CardDetail from "@/components/utility/CardDetail.vue";

console.log('showApi for interested People', allPokemonData);

const filterValue = inject('filterValue');
const selectedPokemon = ref(null);
const filteredPokemon = ref([]);
const filterState = ref('initial');
const openDetail = ref(false);
const itemsPerLoad = 15;
let itemsToDisplay = ref(100);


const handleScroll = (event) => {
  const { scrollTop, scrollHeight, clientHeight } = event.target;
  if (scrollTop + clientHeight >= scrollHeight - 5) {
    // check if max Pokemon is reached
    if (itemsToDisplay.value < allPokemonData[0].length) {
      itemsToDisplay.value += itemsPerLoad;
      // dont load more then available
      if (itemsToDisplay.value > allPokemonData[0].length) {
        itemsToDisplay.value = allPokemonData[0].length;
      }
    }
  }
};

onMounted(async () => {
  await nextTick(); // Warten, bis das DOM vollständig gerendert ist
  const element = document.querySelector("#pokemonIndexArea");
  if (element) {
    element.addEventListener('scroll', handleScroll);
  } else {
    console.error('Element #pokemonIndexArea wurde nicht gefunden.');
  }
});

watch(filterValue, (newValue) => {
  if (newValue === '') {
    filterState.value = 'all';
  } else {
    filterState.value = 'filtered';
  };
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
  };
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
      <card-index
          v-for="(pokemon, index) in (allPokemonData[0] ? allPokemonData[0].slice(0, itemsToDisplay) : [])"
          :key="index" :pokemon="pokemon" @open-pokemon="openPokemon(pokemon)"/>
    </div>
    <div v-if="filterValue" class="filter-wrapper">
      <card-index v-for="(pokemon, index) in filteredPokemon.slice(0, itemsToDisplay)" :key="index"
                  :pokemon="pokemon" @open-pokemon="openPokemon(pokemon)"/>
    </div>
    <!--    <div class="detail-wrapper loading">-->
    <!--      TEST-->
    <!--    </div>-->

    <card-detail :pokemon="selectedPokemon" :visible="openDetail" class="detail-wrapper"
                 @close="closeDetail"></card-detail>
  </div>
</template>

<style lang="scss" scoped>
.index-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  padding: 1rem;
  width: 100%;
  height: 100%;
  position: relative;
  overflow-y: auto;
  max-height: 100vh;

  .detail-wrapper {
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

  .filter-wrapper {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    max-width: 1600px;
    height: 100%;
  }

  .loading {
    z-index: 200;
    background-color: cadetblue;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}

</style>
