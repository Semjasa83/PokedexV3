<script setup>

</script>

<template>
  <div class="card-wrapper">
    <section class="card-header">
      <span>Name</span>
      <span>ID</span>
    </section>
    <section class="card-pic">
      <div class="pic-placeholder"></div>
    </section>
    <section class="card-type">
      <span>Types:</span>

    </section>
  </div>
</template>

<style scoped lang="scss">
.card-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1rem;
  min-width: 12rem;
  min-height: 16rem;
  background-color: hsl(0, 0%, 20%);
  border-radius: 1rem;
}
.pic-placeholder {
  width: 8rem;
  height: 8rem;
  background-color: hsl(0, 0%, 40%);

}
</style>