<script setup>
import '@/js/addWheelListener.js'
import { ref, reactive, onMounted, onUnmounted } from 'vue'

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
  if (activeSection.value < 0) {
    activeSection.value++;
    inMove.value = false;
    return;
  }
  scrollToSection(activeSection.value, true);
}
function moveUp() {
  inMove.value = true;
  activeSection.value++;
  if (activeSection.value > offsets.length - 1) {
    activeSection.value--;
    inMove.value = false;
    return;
  }
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
  window.addWheelListener(window.document, handleMouseWheel);
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
</script>
<template>
  <div>
    <slot></slot>
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
<style lang="scss" scoped>
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
