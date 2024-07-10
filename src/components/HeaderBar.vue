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
  padding: 0 1rem;
  width: 100%;
  background-color: hsl(0, 0%, 20%);

  .header-headline {
    font-size: 2rem;
    font-weight: 600;
    width: fit-content;
    color: #FFFFFF;
    background: hsl(0, 0%, 20%);
    text-shadow: 0 0 5px #fff, 0 0 10px #fff, 0 0 15px #FBA54C, 0 0 20px #FBA54C, 0 0 30px #FBA54C, 0 0 40px #FBA54C, 0 0 55px #FBA54C, 0 0 75px #FBA54C;
  }

  input {
    all: unset;
    background-color: hsl(0, 0%, 70%);
    border-radius: 0.5rem;
    margin: 0.25rem 2rem;
    color: hsl(0, 0%, 20%);
    padding: 0.25rem 1rem;
  }
}

@media (max-width: 500px) {
  .header-wrapper {
    flex-direction: column;
  }
}
</style>