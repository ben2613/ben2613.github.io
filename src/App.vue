<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
// https://codepen.io/WebDEasy/pen/NVOEBL but in vue 3 things
import { ref, reactive, onMounted, onUnmounted } from 'vue'
import 'normalize.css'

const inMove = ref(false);
const activeSection = ref(0);
const offsets = reactive([]);
const touchStartY = ref(0);

function calculateSectionOffsets() {
  let sections = document.getElementsByTagName('section');
  let length = sections.length;
  for (let i = 0; i < length; i++) {
    let sectionOffset = sections[i].offsetTop;
    offsets.push(sectionOffset);
    console.log('section ' + i)
  }
}
function scrollToSection(id, force = false) {
  if (inMove.value && !force) return false;
  activeSection.value = id;
  inMove.value = true;
  document.getElementsByTagName('section')[id].scrollIntoView();
  setTimeout(() => {
    inMove.value = false;
  }, 400);
}
function handleMouseWheel(e) {
  if (e.wheelDelta < 30 && !inMove.value) {
    moveUp();
  } else if (e.wheelDelta > 30 && !inMove.value) {
    moveDown();
  }
  e.preventDefault();
  return false;
}
function handleMouseWheelDOM(e) {
  if (e.detail > 0 && !inMove.value) {
    moveUp();
  } else if (e.detail < 0 && !inMove.value) {
    moveDown();
  }

  return false;
}
function moveDown() {
  inMove.value = true;
  activeSection.value--;
  if (activeSection.value < 0) activeSection.value = offsets.length - 1;
  scrollToSection(activeSection.value, true);
}
function moveUp() {
  inMove.value = true;
  activeSection.value++;
  if (activeSection.value > offsets.length - 1) activeSection.value = 0;
  scrollToSection(activeSection.value, true);
}
function touchStart(e) {
  e.preventDefault();
  touchStartY.value = e.touches[0].clientY;
}
function touchMove(e) {
  if (inMove.value) return false;
  e.preventDefault();
  const currentY = e.touches[0].clientY;
  if (touchStartY.value < currentY) {
    moveDown();
  } else {
    moveUp();
  }
  touchStartY.value = 0;
  return false;
}
onMounted(() => {
  calculateSectionOffsets();
  window.addEventListener('DOMMouseScroll', handleMouseWheelDOM); // Mozilla Firefox
  window.addEventListener('mousewheel', handleMouseWheel, {
    passive: false
  }); // Other browsers
  window.addEventListener('touchstart', touchStart, {
    passive: false
  }); // mobile devices
  window.addEventListener('touchmove', touchMove, {
    passive: false
  }); // mobile devices
})
onUnmounted(() => {
  window.removeEventListener('mousewheel', handleMouseWheel, {
    passive: false
  }); // Other browsers
  window.removeEventListener('DOMMouseScroll', handleMouseWheelDOM); // Mozilla Firefox
  window.removeEventListener('touchstart', touchStart); // mobile devices
  window.removeEventListener('touchmove', touchMove); // mobile devices
})

import Construction from '@/components/Contructing.vue';
import Page from '@/components/Page.vue'
</script>

<template>
  <div id="app">
    <Page class="blue">
      <Construction />
    </Page>
    <Page class="black">
      <h1>Section 2</h1>
    </Page>
    <Page class="green">
      <h1>Section 3</h1>
    </Page>
    <Page class="blue">
      <h1>Section 4</h1>
    </Page>
    <div class="sections-menu">
      <span
        class="menu-point"
        :class="{ active: activeSection == index }"
        @click="scrollToSection(index)"
        v-for="(offset, index) in offsets"
        :key="index"
      ></span>
    </div>
  </div>
</template>

<style>
html {
  scroll-behavior: smooth;
}
body {
  margin: 0;
  overflow: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
h1 {
  font-size: 6em;
  margin: 0;
  text-align: center;
  padding: 0 1rem;
}
.sections-menu {
  position: fixed;
  right: 1rem;
  top: 50%;
  transform: translateY(-50%);
}
.sections-menu .menu-point {
  width: 10px;
  height: 10px;
  background-color: #fff;
  display: block;
  margin: 1rem 0;
  opacity: 0.6;
  transition: 0.4s ease all;
}
.sections-menu .menu-point.active {
  opacity: 1;
  transform: scale(1.5);
}
</style>
