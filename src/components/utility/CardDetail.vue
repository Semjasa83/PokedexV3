<script setup>

import { watch } from 'vue';

const props = defineProps({
  visible: {
    type: Boolean,
    default: false
  },
  pokemon: {
    type: Object,
    default: () => ({})
  }
});

const emit = defineEmits(['close']);

watch(() => props.visible, (newValue) => {
  console.log('Dialog visibility changed to:', newValue);
});

const closeDialog = () => {
  console.log('Closing dialog');
  emit('close');
};
</script>

<template>
  <div v-if="visible" class="dialog">
    <div class="card-wrapper">
      <h2>{{ pokemon?.name || 'No Pokemon selected' }}</h2>
      <!-- Fügen Sie hier weitere Details des Pokémon hinzu -->
      <button @click="closeDialog">Schließen</button>
    </div>
  </div>
</template>

<style scoped lang="scss">
  .dialog{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    width: 100%;
    background-color: #33333399;
   backdrop-filter: blur(3px);
  }

  .card-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 30rem;
    width: 20rem;
    background-color: grey;
  }

</style>