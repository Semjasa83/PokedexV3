<script>
import axios from 'axios';
import {reactive} from "vue";

export const allPokemon = reactive([]);
let offset = 0;
let limit = 100;

export default {
  name: "ApiService"
}

export async function getAllPokemon() {
  const response = await axios.get(`https://pokeapi.co/api/v2/pokemon?limit=${limit}&offset=${offset}`);
  const pokemonData = await Promise.all(response.data.results.map(async (pokemon) => {
    const additionalData = await getPokemonData(pokemon.url);
    return {...pokemon, additionalData};
  }));
  allPokemon.value = pokemonData;
}

async function getPokemonData(url) {
  const response = await axios.get(url);
  return response.data;
}


// export async function getAllPokemon() {
//   ....
//   getPokemonIndexImg(pokemonData);
// }
// async function getPokemonIndexImg(pokemonData) {
//   const pokemonImg = await Promise.all(pokemonData.map(async (pokemon) => {
//     const img = await axios.get(pokemon.additionalData.sprites.front_default);
//     return { ...pokemon, img };
//   }));
//   allPokemon.value = pokemonImg;
// }
getAllPokemon();


</script>

