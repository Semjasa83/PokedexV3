<script setup>
import {ref, watch} from 'vue';
import AboutStats from './AboutStats.vue';
import BaseStats from './BaseStats.vue';
import MovesStats from './MovesStats.vue';

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

watch(() => props.visible, () => {
});

const closeDialog = () => {
  emit('close');
};

const noCloseDialog = () => {
};

const currentSection = ref('aboutStats'); // Mögliche Werte: 'about', 'baseStats', 'moves'

</script>

<template>
  <div v-if="visible" class="dialog" @click="closeDialog">
    <div :class="pokemon.additionalData.types[0].type.name + '-border'" class="card-wrapper"
         @click.stop="noCloseDialog">
      <section class="upper-section">
        <img alt="icon" class="close-icon" src="../../assets/icons/close.svg" @click="closeDialog">
        <span class="poke-name">{{ pokemon?.name || 'No Pokemon selected' }}</span>
        <div class="card-type">
          <span v-for="(types, index) in pokemon.additionalData.types" :key="index" :class="types.type.name">
          {{ types.type.name }}
          </span>
        </div>
        <img :src="pokemon.additionalData.sprites.other.dream_world.front_default" alt="Pokemon Img"
             class="pokemon-img"
             loading="lazy">
        <span class="pokemon-id">#{{pokemon.additionalData.id}}</span>

      </section>
      <section class="center-section">
        <a @click="currentSection = 'aboutStats'" :class="{ active: currentSection === 'aboutStats' }">About</a>
        <a @click="currentSection = 'baseStats'" :class="{ active: currentSection === 'baseStats' }">Base Stats</a>
        <a @click="currentSection = 'movesStats'" :class="{ active: currentSection === 'movesStats' }">Moves</a>
      </section>
      <div class="lower-section">
        <AboutStats v-if="currentSection === 'aboutStats'" :pokemon="pokemon"/>
        <BaseStats v-if="currentSection === 'baseStats'" :pokemon="pokemon"/>
        <MovesStats v-if="currentSection === 'movesStats'" :pokemon="pokemon"/>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.dialog {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
  background-color: #33333399;
  backdrop-filter: blur(3px);
}

.card-wrapper {
  border-radius: 1rem;
  display: flex;
  flex-direction: column;
  height: 35rem;
  width: 25rem;
  background-color: hsl(0, 0%, 20%);

  .poke-name {
    margin-top: 1rem;
    font-size: 1.5rem;
    font-weight: 600;
    text-transform: capitalize;
  }

  .close-icon {
    position: absolute;
    top: 1rem;
    right: 1rem;
    height: 1.5rem;
    width: 1.5rem;
    cursor: pointer;
  }
}

.upper-section {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  height: 55%;
  background-color: hsl(0, 0%, 20%);
  border-radius: 1rem 1rem 0 0;
  position: relative;

  .upper-section-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .card-type {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    width: 100%;

    span {
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 0.5rem;
      margin: 0.5rem;
      border-radius: 1rem;
      min-width: 5rem;
      color: #282828;
      font-weight: 700;
      text-transform: capitalize;
    }
  }

  .pokemon-id{
    position: absolute;
    right: 1rem;
    bottom: 1rem;
  }

  .pokemon-img {
    position: absolute;
    height: 60%;
    padding: 0.5rem;
    bottom: 0;
  }
}

.center-section {
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 2rem;
  align-items: center;
  height: 7%;
  background-color: hsl(0, 0%, 50%);
  border-radius: 1rem 1rem 0 0;
  border-bottom: 0.5px solid hsl(0, 0%, 50%);
  a {
    text-align: center;
    font-weight: 700;
    width: 100%;
    cursor: pointer;
    border-bottom: 3px solid hsl(0, 0%, 50%);
    padding: 0.25rem 0;
    &:hover {
      color: hsl(0, 0%, 20%);
      border-bottom: 3px solid hsl(0, 0%, 70%);
    }
  }
}

.lower-section {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: start;
  height: 50%;
  background-color: hsl(0, 0%, 100%);
  border-radius: 0 0 1rem 1rem;
  overflow-y: auto;
  gap: 1rem;
  padding: 0.5rem;
  color: hsl(0, 0%, 20%);
}

.active {
  color: hsl(0, 0%, 20%);
  border-bottom: 3px solid hsl(0, 0%, 20%) !important;
}

</style>