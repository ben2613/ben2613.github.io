<script setup>
import data from '@/assets/json/task_can_do.json'

function getImgUrl(name) {
  return new URL(`../../assets/${name}`, import.meta.url)
}
</script>
<template>
  <div pt-30>
    <!-- List all tasks with short desc + optional img -->
    <h2>What I can do</h2>
    <div class="flex items-center" :class="(i % 2 === 0) ? '' : 'flex-row-reverse'" v-for="(datum, i) in data" :key="i">
      <img class="max-w-50% sm:max-w-40% lg:max-w-30% max-h-33vh" :src="getImgUrl(datum.img)" :alt="datum.desc" />
      <p class>{{ datum.desc }}</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
</style>
