<script>
import axios from 'axios';
import {reactive} from "vue";

export const allPokemon = reactive([]);

export default {
  name: "ApiService"
}

async function getPokemonData(url) {
  const response = await axios.get(url);
  return response.data;
}

export async function getAllPokemon() {
  const response = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=100');
  const pokemonData = await Promise.all(response.data.results.map(async (pokemon) => {
    const additionalData = await getPokemonData(pokemon.url);
    return { ...pokemon, additionalData };
  }));
  const pokemonImg = await Promise.all(pokemonData.map(async (pokemon) => {
    const img = await axios.get(pokemon.additionalData.sprites.other.dream_world.front_default);
    return { ...pokemon, img };
  }));
  allPokemon.value = pokemonImg;
}

getAllPokemon();

</script>

