<script setup>
defineProps({
  pokemon: Object
});

</script>

<template>
  <div class="move" v-for="(pokeStats, index) in (pokemon.additionalData.moves)" :key="index" :pokeStats="pokeStats">
    {{ pokeStats.move.name }}
  </div>
</template>

<style scoped lang="scss">
  .move {
    padding: 0.25rem 0.5rem;
    border-radius: 1rem;
    background-color: hsl(0, 1%, 60%);
  }
</style>