<script setup>
import { inject } from 'vue';

const handleFilterRef = inject('handleFilter');

function filterPokemon(event) {
  if (handleFilterRef && typeof handleFilterRef.value === 'function') {
    handleFilterRef.value(event.target.value);
  } else {
    console.error('handleFilter is not a function');
  }
}
</script>

<template>
  <div class="header-wrapper">
    <span class="header-headline">Pokedex</span>
    <input type="text" @keyup="filterPokemon" maxlength="20" placeholder="search by name">
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

  input {
    all: unset;
    background-color: hsl(0, 0%, 70%);
    border-radius: 0.5rem;
    margin: 0 2rem;
    height: 2rem;
    color: hsl(0, 0%, 20%);
    padding: 0 1rem;
  }
}
</style>