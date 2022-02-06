<script setup>
import { computed } from 'vue'
import { useGlobalState } from '@/store'
import { useToggle } from '@vueuse/core'
defineProps({
  items: Array, // [{id, display}, ...]
})
const emit = defineEmits(['menu'])
const onclick = (i) => { emit('menu', i); console.log(`Clicked ${i}`) }
const state = useGlobalState()
const toggleLuxury = useToggle(state)
const effectOn = computed(() => state.value)
</script>
<template>
  <nav class="fixed top-0 right-0">
    <ul class="flex flex-wrap list-none m-0 p-5 bg-transparent">
      <li class="mx-3 p-1 text-center" v-for="(item, index) in items" :key="index">
        <a
          class="inline-block whitespace-nowrap text-lg text-white no-underline visited:text-white hover:animate-pulse"
          :class="effectOn ? 'hover:animate-ping' : ''"
          href="#"
          @click.prevent="onclick(index)"
        >{{ item.props.display }}</a>
      </li>
      <!-- Toggle luxury mode -->
      <li>
        <button
          class="cursor-point rounded"
          :class="effectOn ? 'bg-green' : 'bg-red'"
          @click="toggleLuxury()"
        >Toggle Luxury Mode</button>
      </li>
    </ul>
  </nav>
</template>
<style lang="scss" scoped>
a::after {
  transition: all ease-out;
  content: "";
  width: 0px;
  height: 1px;
  display: block;
  background: white;
  transition: 300ms;
  margin: auto;
}
a:hover::after {
  width: 100%;
}
</style>
