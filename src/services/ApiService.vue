<script>
import axios from 'axios';
import {reactive} from "vue";

export const allPokemon = reactive([]);
export const allPokemonWithData = reactive([]);
let offset = 0;
let limit = 1302;

export default {
  name: "ApiService"
}

export async function getAllPokemon() {
  const response = await axios.get(`https://pokeapi.co/api/v2/pokemon?limit=${limit}&offset=${offset}`);
  allPokemon.value = response.data.results; // Assign the results to allPokemon.value
}

export async function addAdditionalData() {
  const allPokemonWithAdditionalData = await Promise.all(allPokemon.value.map(async (pokemon) => {
    const additionalData = await getPokemonData(pokemon.url);
    return {...pokemon, additionalData};
  }));
  // return allPokemonWithAdditionalData;
  allPokemonWithData.push(allPokemonWithAdditionalData);
}

async function getPokemonData(url) {
  try {
    const response = await axios.get(url);
    return response.data;
  } catch (error) {
    console.error(`Failed to fetch data from ${url}:`, error);
    return null;
  }
}

async function fetchData() {
  await getAllPokemon();
  addAdditionalData();
}

fetchData();
console.log(allPokemonWithData) //LOG DELETE LATER
</script>

