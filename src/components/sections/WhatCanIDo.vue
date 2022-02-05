<script setup>
import data from '@/assets/json/task_can_do.json'

</script>
<template>
  <div flex flex-wrap>
    <!-- List all tasks with short desc + optional img -->
    <div v-for="(datum, i) in data" :key="i">
      <p>{{ datum.desc }}</p>
      <img class="h-33vh" :src="`src/assets/${datum.img}`" :alt="datum.desc" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
</style>
