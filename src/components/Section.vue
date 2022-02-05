<script setup>
defineProps({
  display: String, // display in the menu
  multiPage: Boolean, // to let the script
})
</script>
<template>
  <section :class="multiPage ? 'multi-page' : 'h-100vh'">
    <slot></slot>
  </section>
</template>
<style lang="scss">
section {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  color: #ccc;
  &.black {
    background-color: #040303;
  }

  &.blue {
    background-color: #41729f;
  }

  &.green {
    background-color: #5c7457;
  }

  &.red {
    background-color: #984447;
  }

  &.brown {
    background-color: #846333;
  }
}
</style>
