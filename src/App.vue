<script setup>
import HeaderBar from './components/HeaderBar.vue'
import PokedexIndex from "@/components/PokedexIndex.vue";
</script>

<template>
  <div class="home-wrapper">
    <div class="header-wrapper">
      <header-bar />
    </div>
    <div class="content-wrapper">
      <pokedex-index />
    </div>

  </div>
</template>

<style scoped lang="scss">
  .home-wrapper {
    display: flex;
    flex-direction: column;
    height: 100vh;
    width: 100%;
    overflow: hidden;
    background-color: hsl(0, 0%, 40%);
  }

  .header-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 6rem;
  }

  .content-wrapper {
    display: flex;
    justify-content: center;
    width: 100%;
    overflow-y: auto;
  }

  /* Scroll bar stylings */
  ::-webkit-scrollbar {
    width: 12px;
    height: 10px;
  }

  /* Track */
  ::-webkit-scrollbar-track {
    background: hsl(0, 0%, 20%);
  }

  /* Handle */
  ::-webkit-scrollbar-thumb {
    background:  hsl(0, 0%, 30%);
    border-radius: 5px;
  }

  /* Handle on hover */
  ::-webkit-scrollbar-thumb:hover {
    background: hsl(0, 0%, 40%);
  }
</style>
