<script setup>
defineProps({
  multiPage: Boolean, // to let the script
});
</script>
<template>
  <section :class="multiPage ? 'multi-page' :'h-100vh' ">
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
  &.black {
    background-color: #000;
  }

  &.blue {
    background-color: #41729f;
    color: #c3e0e5;
  }

  &.green {
    background-color: #68c368;
  }
}
</style>
