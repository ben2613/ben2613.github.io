<script setup>
defineProps({
  items: Array, // [{id, display}, ...]
})
const emit = defineEmits(['menu'])
const onclick = (i) => { emit('menu', i); console.log(`Clicked ${i}`) }
</script>
<template>
  <nav class="fixed top-0 right-0">
    <ul class="flex flex-wrap list-none m-0 p-5 bg-transparent">
      <li class="mx-3 p-1 text-center" v-for="(item, index) in items" :key="index">
        <a
          class="whitespace-nowrap text-lg text-white no-underline visited:text-white"
          href="#"
          @click.prevent="onclick(index)"
        >{{ item.props.display }}</a>
      </li>
    </ul>
    <!-- Toggle luxury mode -->
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
