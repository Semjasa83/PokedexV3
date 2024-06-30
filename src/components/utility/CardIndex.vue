<script>
import axios from "axios";
import {onMounted, ref} from "vue";

export default {
  name: "CardIndex",
  props: {
    pokemon: {
      type: Object,
      required: true
    }
  },
  setup(props) {
    const pokemonImg = ref(null);
    onMounted(async () => {
      const response = await axios.get(`https://pokeapi.co/api/v2/pokemon/${props.pokemon.additionalData.id}`);
      pokemonImg.value = response.data.sprites.front_default;
    });
    return {
      pokemonImg
    };
  }
}

</script>

<template>
  <div class="card-wrapper" :class="pokemon.additionalData.types[0].type.name + '-border'">
    <section class="card-header">
      <span class="poke-name">{{ pokemon.name }}</span>
      <span class="poke-id">#{{ pokemon.additionalData.id }}</span>
    </section>
    <section class="card-pic">
      <img class="pokemon-img" :src="pokemonImg" alt="Pokemon Img" loading="lazy">
    </section>
  <section class="card-type">
    <span v-for="(types, index) in pokemon.additionalData.types" :key="index" :types="types" :class="types.type.name">
      {{ types.type.name }}
    </span>
  </section>
  </div>
</template>

<style scoped lang="scss">
.card-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  min-width: 14rem;
  min-height: 18rem;
  background-color: hsl(0, 0%, 20%);
  border-radius: 1rem;
  margin: 1rem;
  position: relative;
  border: 2px solid hsl(0, 0%, 100%);
  .card-header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    height: 100%;
    width: 100%;
    .poke-name {
      text-transform: capitalize;
      font-weight: 700;
      font-size: 1.2rem;
    }
    .poke-id {
      //position: absolute;
      top: 0.5rem;
      right: 1rem;
    }
  }
  .card-pic {
    width: 8rem;
    height: 8rem;
    object-fit: contain;
    img {
      width: 100%;
      height: 100%;
    }
  }
  .card-type {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    width: 100%;
    span {
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 0.5rem;
      margin: 0.5rem;
      border-radius: 1rem;
      min-width: 4rem;
      color: #282828;
      font-weight: 700;
      text-transform: capitalize;
    }
  }
}

</style>