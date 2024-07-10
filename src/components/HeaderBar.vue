<script setup>
function filterPokemon(event) {
  console.log(event.target.value);
}
</script>

<template>
  <div class="header-wrapper">
    <span class="header-headline">Pokedex</span>
    <input type="text" @keyup="filterPokemon">
  </div>

</template>


<style lang="scss">
.header-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 6rem;
  padding: 1rem;
  width: 100%;
  background-color: hsl(0, 0%, 20%);

  .header-headline {
    font-size: 2rem;
    font-weight: 600;
    color: red;
    width: fit-content;
  }
}
</style>