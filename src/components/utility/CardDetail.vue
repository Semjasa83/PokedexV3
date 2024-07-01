<script>

export default {
  name: "CardDetail",
  props: {
    open: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<template>
  <dialog v-if="open">
    test
  </dialog>
</template>

<style scoped lang="scss">
  dialog{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    width: 100%;
    background-color: #33333399;
   backdrop-filter: blur(3px);
  }

</style>