<script setup>
defineProps({
  items: Array, // [{id, display}, ...]
})
const emit = defineEmits(['menu'])
const onclick = (i) => { emit('menu', i); console.log(`Clicked ${i}`) }
</script>
<template>
  <div class="menu">
    <ul>
      <li v-for="(item, index) in items" :key="index">
        <button @click="onclick(index)">{{ item.props.display }}</button>
      </li>
    </ul>
  </div>
</template>
<style lang="scss" scoped>
.menu {
  position: fixed;
  right: 1rem;
  top: 1rem;
}
</style>
