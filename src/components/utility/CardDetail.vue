<script>

import {toRefs, watch} from "vue";

export default {
  name: "CardDetail",
  props: {
    visible: {
      type: Boolean,
      default: false
    },
    pokemon: Object
  },
  setup(props) {
    const { visible} = toRefs(props);

    watch(visible, (newValue, oldValue) => {
      console.log('open prop changed from', oldValue, 'to', newValue);
    });
  }
}
</script>

<template>
  <div v-if="visible" class="dialog">
      <div class="card-wrapper">

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