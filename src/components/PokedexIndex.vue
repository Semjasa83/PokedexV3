<script setup>
import { ref, onMounted } from 'vue';
import CardIndex from "@/components/utility/CardIndex.vue";
import { allPokemonData } from "@/services/ApiService.vue";
import CardDetail from "@/components/utility/CardDetail.vue";

console.log('pokeindex', allPokemonData);

let itemsToDisplay = ref(10);
const itemsPerLoad = 10;
let openDetail = ref(false);
const selectedPokemon = ref(null);

onMounted(() => {
  window.addEventListener('scroll', () => {
    if ((window.innerHeight + window.scrollY) >= document.body.offsetHeight) {
      itemsToDisplay.value += itemsPerLoad;
    }
  });
});

const openPokemon = (pokemon) => {
  console.log('Pokemon ID:', pokemon);
  selectedPokemon.value = pokemon;
  openDetail.value = true;
  console.log(openDetail.value)
  // Hier können Sie den Code hinzufügen, um die Pokemon Details zu öffnen
};

const closeDetail = () => {
  openDetail.value = false;
  selectedPokemon.value = null;
  console.log('Closing detail, openDetail is now:', openDetail.value);
};

</script>

<template>
  <div id="pokemonIndexArea" class="index-wrapper">
    <card-index v-for="(pokemon, index) in (allPokemonData[0] ? allPokemonData[0].slice(0, itemsToDisplay.value) : [])" :key="index" :pokemon="pokemon"  @open-pokemon="openPokemon(pokemon)" />
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
    position: absolute;
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


</style>
