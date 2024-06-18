<script>
import axios from 'axios';

const allPokemon = [];

export default {
  name: "ApiService"
}



async function getPokemonData(url) {
  const response = await axios.get(url);
  return response.data;
}

export async function getAllPokemon() {
  const response = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=151');
  const pokemonData = await Promise.all(response.data.results.map(async (pokemon) => {
    const additionalData = await getPokemonData(pokemon.url);
    return { ...pokemon, additionalData };
  }));
  allPokemon.value = pokemonData;
}

console.log(allPokemon);

</script>

