<script setup>
import { watch, ref } from 'vue';
import axios from 'axios';

const props = defineProps({
  pokemon: Object
});

let speciesData = ref({});
watch(() => props.pokemon, async (newVal) => {
  if (newVal && newVal.additionalData) {
    const id = newVal.additionalData.id;
    const fetchSpecies = await axios.get(`https://pokeapi.co/api/v2/pokemon-species/${id}/`)
    speciesData.value = fetchSpecies.data.egg_groups;
  }
}, { immediate: true });

</script>

<template>
<!--   <div>-->
<!--    <div class="stat">-->
<!--      <span class="stat-name">Height: </span>-->
<!--      <span class="stat-value">{{ pokemon.additionalData.height * 10 }} cm</span>-->
<!--    </div>-->
<!--    <div class="stat">-->
<!--      <span class="stat-name">Weight: </span>-->
<!--      <span class="stat-value">{{ pokemon.additionalData.weight / 10 }} kg</span>-->
<!--    </div>-->
<!--    <div class="stat">-->
<!--      <span class="stat-name">Base Experience: </span>-->
<!--      <span class="stat-value">{{ pokemon.additionalData.base_experience }} xp</span>-->
<!--    </div>-->
<!--    <div class="stat">-->
<!--      <span class="stat-name">Egg Group: </span>-->
<!--      <div class="species">-->
<!--        <span class="stat-value" v-for="(item, index) in speciesData" :key="index">{{ item.name }}</span>-->
<!--      </div>-->
<!--    </div>-->
<!--  </div>-->

  <div>
    <table>
      <tr>
        <td><span class="stat-name">Height: </span></td>
        <td><span class="stat-value">{{ pokemon.additionalData.height * 10 }} cm</span></td>
      </tr>
      <tr>
        <td><span class="stat-name">Weight: </span></td>
        <td><span class="stat-value">{{ pokemon.additionalData.weight / 10 }} kg</span></td>
      </tr>
      <tr>
        <td><span class="stat-name">Base Exp: </span></td>
        <td><span class="stat-value">{{ pokemon.additionalData.base_experience }} xp</span></td>
      </tr>
      <tr>
        <td><span class="stat-name">Egg Group: </span></td>
        <td>
          <div class="species">
            <span class="stat-value" v-for="(item, index) in speciesData" :key="index">{{ item.name }}</span>
          </div>
        </td>
      </tr>
    </table>
  </div>
</template>

<style scoped lang="scss">
// .stat {
  // display: flex;
  // flex-direction: row;

  .stat-name {
    display: flex;
    align-items: start;
    text-align: start;
    font-weight: bold;
    margin-right: 0.5rem;
    height: fit-content;
  }

  .species {
    display: flex;
    flex-direction: column;
  }
// }
</style>