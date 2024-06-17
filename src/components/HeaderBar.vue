<template>

  <div class="header-wrapper">
    <span class="header-headline">Pokedex</span>
  </div>


</template>

<script>
export default {}
</script>

<style lang="scss">
.header-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: fit-content;
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