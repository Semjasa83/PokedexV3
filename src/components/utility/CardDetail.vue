<script setup>

import {watch} from 'vue';

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

</script>

<template>
  <div v-if="visible" class="dialog" @click="closeDialog">
    <div class="card-wrapper" @click.stop="noCloseDialog"
         :class="pokemon.additionalData.types[0].type.name + '-border'">
      <img src="../../assets/icons/close.svg" alt="icon" class="close-icon">
      <span class="poke-name">{{ pokemon?.name || 'No Pokemon selected' }}</span>
      <section class="upper-section">
        <div class="card-type">
          <span v-for="(types, index) in pokemon.additionalData.types" :key="index" :class="types.type.name">
          {{ types.type.name }}
        </span>
        </div>
        <img class="pokemon-img" :src="pokemon.additionalData.sprites.other.dream_world.front_default" alt="Pokemon Img"
             loading="lazy">
      </section>
      <section class="center-section">

      </section>
      <section class="lower-section">

      </section>


    </div>
  </div>
</template>

<style scoped lang="scss">
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
  padding: 1rem;
  position: relative;

  .poke-name {
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
  }
}

.upper-section {
  margin-top: 0.5rem;
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  height: 45%;
  border: 1px solid hsl(0, 0%, 50%);
  background-color: hsl(0, 0%, 40%);
  border-radius: 1rem 1rem 0 0;

  .card-type {
    display: flex;
    flex-direction: column;
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

  .pokemon-img {
    width: 60%;
    padding: 0.5rem;
  }
}

.center-section {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 10%;
  background-color: hsl(0, 0%, 20%);
}

.lower-section {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 45%;
  border: 1px solid hsl(0, 0%, 50%);
  background-color: hsl(0, 0%, 40%);
  border-radius: 0 0 1rem 1rem;
}



</style>