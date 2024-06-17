<script>

let allPokemon = [];

export default {
  name: "ApiService"
}

export async function getAllPokemon() {
  const url = "https://pokeapi.co/api/v2/pokemon?limit=1500";
  let response = await fetch(url);
  let responseAsJson = await response.json();
  allPokemon = responseAsJson.results;
  console.log(allPokemon);
}
</script>

