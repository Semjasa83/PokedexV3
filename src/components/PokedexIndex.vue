<script setup>
import {ref, onMounted, watch, inject, onUnmounted, nextTick} from 'vue';
import CardIndex from "@/components/utility/CardIndex.vue";
import {allPokemonData} from "@/services/ApiService.vue";
import CardDetail from "@/components/utility/CardDetail.vue";
import {showLoading} from "@/services/ApiService.vue";

console.log('showApi for interested People', allPokemonData);

const filterValue = inject('filterValue');
const selectedPokemon = ref(null);
const filteredPokemon = ref([]);
const filterState = ref('');
const openDetail = ref(false);
const itemsPerLoad = 15;
let itemsToDisplay = ref(100);


const handleScroll = (event) => {
  const {scrollTop, scrollHeight, clientHeight} = event.target;
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
  }
  ;
  switch (filterState.value) {
    case 'filtered':
      filteredPokemon.value = allPokemonData[0].filter(pokemon => pokemon.name.toLowerCase().includes(newValue.toLowerCase()));
      break;
    case 'all':
      filteredPokemon.value = allPokemonData[0];
      break;
  }
  ;
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
    <div class="detail-wrapper loading" v-if="showLoading">
      <span class="loading-headline">Pokedex</span>
      <span class="loader"></span>
    </div>

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
    background-color: hsl(0, 0%, 20%);
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}

.loader {
  z-index: 350;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  position: relative;
  animation: rotate 1s linear infinite
}
.loader::before , .loader::after {
  content: "";
  box-sizing: border-box;
  position: absolute;
  inset: 0px;
  border-radius: 50%;
  border: 5px solid #FFF;
  animation: prixClipFix 2s linear infinite ;
}
.loader::after{
  inset: 8px;
  transform: rotate3d(90, 90, 0, 180deg );
  border-color: #FF3D00;
}

@keyframes rotate {
  0%   {transform: rotate(0deg)}
  100%   {transform: rotate(360deg)}
}

@keyframes prixClipFix {
  0%   {clip-path:polygon(50% 50%,0 0,0 0,0 0,0 0,0 0)}
  50%  {clip-path:polygon(50% 50%,0 0,100% 0,100% 0,100% 0,100% 0)}
  75%, 100%  {clip-path:polygon(50% 50%,0 0,100% 0,100% 100%,100% 100%,100% 100%)}
}

.loading-headline {
  font-size: 4rem;
  font-weight: 600;
  width: fit-content;
  color: #FFFFFF;
  background: hsl(0, 0%, 20%);
  text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #FBA54C, 0 0 20px #FBA54C, 0 0 30px #FBA54C, 0 0 40px #FBA54C, 0 0 55px #FBA54C, 0 0 75px #FBA54C;
}

</style>
