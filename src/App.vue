<script setup>
/*import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'*/
import HeaderBar from './components/HeaderBar.vue'
import PokedexIndex from "@/components/PokedexIndex.vue";
</script>

<template>
  <div class="home-wrapper">
    <header-bar />
    <pokedex-index />
  </div>

<!--  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>-->
</template>

<style scoped lang="scss">
  .home-wrapper {
    display: flex;
    flex-direction: column;
    height: 100vh;
    width: 100%;
  }
</style>
