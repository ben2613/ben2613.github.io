<script setup>
import { ref } from 'vue'
import { useElementVisibility } from '@vueuse/core'

defineProps({
  display: String, // display in the menu
  multiPage: Boolean, // to let the script
})
const target = ref(null)
const isVisible = useElementVisibility(target)
</script>
<template>
  <section class="relative" :class="[multiPage ? 'multi-page' : 'h-100vh']">
    <!-- for detect if some part of this region is entered-->
    <div ref="target" class="absolute top-25vh bottom-25vh"></div>
    <div class="transition-opacity ease-in-out duration-1000" :class="isVisible ? 'opacity-100' : 'opacity-0'">
      <slot></slot>
    </div>
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
