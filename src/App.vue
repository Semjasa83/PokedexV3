<script setup>
/*import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'*/
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
</style>
