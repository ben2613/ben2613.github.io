<script setup>
import { ref, reactive, onBeforeUpdate, nextTick } from 'vue'
import { useElementVisibility } from '@vueuse/core'
import data from '@/assets/json/task_can_do.json'

function getImgUrl(name) {
  return new URL(`../../assets/${name}`, import.meta.url)
}
const divs = reactive([])
const isVisibles = reactive([])
onBeforeUpdate(() => {
  divs.splice(0, divs.length)
})

nextTick(() => {
  divs.forEach(d => {
    // console.log('try insert')
    let v = useElementVisibility(d)
    // console.log(isVisibles)
    isVisibles.push(v)
    // console.log(isVisibles)
  })
})

</script>
<template>
  <div pt-30>
    <!-- List all tasks with short desc + optional img -->
    <h2>What I can do</h2>
    <div
      :ref="el => { if (el) divs[i] = ref(el) }"
      :class="[
        'flex',
        'items-center',
        'transition-all',
        'duration-750',
        'ease-linear',
        isVisibles.length === 0 ? '' :
          (isVisibles[i].value ? 'translate-x-0 opacity-100' : (i % 2 === 0) ? 'translate-x-full opacity-0' : '-translate-x-full opacity-0'),
        (i % 2 === 0) ? '' : 'flex-row-reverse'
      ]"
      v-for="(datum, i) in data"
      :key="i"
    >
      <img
        @load="onload"
        class="max-w-50% sm:max-w-40% lg:max-w-30% max-h-33vh"
        :src="getImgUrl(datum.img)"
        :alt="datum.desc"
      />
      <p class>{{ datum.desc }}</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
</style>
