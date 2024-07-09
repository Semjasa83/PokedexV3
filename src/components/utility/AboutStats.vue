<script setup>
const props = defineProps({
  pokemon: Object
});

</script>

<template>
  <div class="lower-content">
    <table>
      <tr>
        <td class="table-headline">
          <span class="stat-name">Height: </span>
        </td>
        <td class="table-content">
          <span class="stat-value">{{ pokemon.additionalData.height * 10 }} cm</span>
        </td>
      </tr>
      <tr>
        <td class="table-headline">
          <span class="stat-name">Weight: </span>
        </td>
        <td class="table-content">
          <span class="stat-value">{{ pokemon.additionalData.weight / 10 }} kg</span>
        </td>
      </tr>
      <tr>
        <td class="table-headline">
          <span class="stat-name">Base Exp: </span>
        </td>
        <td class="table-content">
          <span class="stat-value">{{ pokemon.additionalData.base_experience }} xp</span>
        </td>
      </tr>
      <tr>
        <td class="table-headline">
          <span class="stat-name">Abilities: </span>
        </td>
        <td class="table-content">
          <div class="abilities">
            <span v-for="(item, index) in pokemon.additionalData.abilities" :key="index" class="stat-value">{{ item.ability.name }}</span>
          </div>
        </td>
      </tr>
    </table>
  </div>
</template>

<style lang="scss" scoped>

.stat-name {
  display: flex;
  align-items: start;
  text-align: start;
  font-weight: bold;
  margin-right: 0.5rem;
  height: fit-content;
}

.table-headline {
  display: flex;
}

.abilities {
  display: flex;
  flex-direction: column;
}

</style>