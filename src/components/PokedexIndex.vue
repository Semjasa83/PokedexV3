<script setup>
import IndexCard from "@/components/IndexCard.vue";
import { getAllPokemon } from "../services/ApiService.vue";
getAllPokemon();
</script>

<template>
  <div class="index-wrapper">
    <index-card />
  </div>
</template>

<style scoped>
.index-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1rem;
  width: 100%;
  height: 100%;
  background-color: hsl(0, 0%, 40%);
}
</style>