<script setup>
import { ref, reactive, onMounted, onUnmounted } from "vue"
import debounce from 'lodash/debounce'
import Menu from "./Menu.vue"

const inMove = ref(false)
const activeSection = ref(0)
const offsets = reactive([])
const isMultiPage = reactive([]) // this should be same length with offsets
const touchStartY = ref(0)

function resetAll() {
  offsets.splice(0, offsets.length)
  isMultiPage.splice(0, isMultiPage.length)
}
function calculateSectionOffsets() {
  let sections = document.getElementsByTagName("section")
  let length = sections.length
  for (let i = 0; i < length; i++) {
    let sectionOffset = sections[i].offsetTop
    offsets.push(sectionOffset)
    isMultiPage.push(sections[i].classList.contains("multi-page"))
    console.log("section " + i)
  }
}
function scrollToSection(id, force = false) {
  if (inMove.value && !force) return false
  activeSection.value = id
  inMove.value = true
  document.getElementsByTagName("section")[id].scrollIntoView()
  setTimeout(() => {
    inMove.value = false
  }, 400)
}
function handleMouseWheel(e) {
  if (e.wheelDelta < 30 && !inMove.value) {
    moveDown()
  } else if (e.wheelDelta > 30 && !inMove.value) {
    moveUp()
  }
  e.preventDefault()
  return false
}
function moveUp() {
  if (
    isMultiPage[activeSection.value] &&
    !(Math.trunc(window.pageYOffset) <= offsets[activeSection.value])
  ) {
    _moveUpABit()
  } else {
    _moveUp()
  }
}
function _moveUpABit() {
  inMove.value = true
  window.scrollTo(
    window.pageXOffset,
    Math.round(
      window.pageYOffset - (1 / 2) * document.documentElement.clientHeight
    )
  )
  setTimeout(() => {
    inMove.value = false
  }, 400)
}
function _moveUp() {
  inMove.value = true
  activeSection.value--
  if (activeSection.value < 0) {
    activeSection.value++
    inMove.value = false
    return
  }
  scrollToSection(activeSection.value, true)
}
function moveDown() {
  if (
    activeSection.value < offsets.length - 1 &&
    isMultiPage[activeSection.value] &&
    Math.trunc(window.pageYOffset + document.documentElement.clientHeight) < offsets[activeSection.value + 1]
  ) {
    _moveDownABit()
  } else {
    _moveDown()
  }
}
function _moveDownABit() {
  inMove.value = true
  window.scrollTo(
    window.pageXOffset,
    Math.round(
      window.pageYOffset + (1 / 2) * document.documentElement.clientHeight
    )
  )
  setTimeout(() => {
    inMove.value = false
  }, 400)
}
function _moveDown() {
  inMove.value = true
  activeSection.value++
  if (activeSection.value > offsets.length - 1) {
    activeSection.value--
    inMove.value = false
    return
  }
  scrollToSection(activeSection.value, true)
}
function touchStart(e) {
  e.preventDefault()
  touchStartY.value = e.touches[0].clientY
}
function touchMove(e) {
  if (inMove.value) return false
  e.preventDefault()
  const currentY = e.touches[0].clientY
  if (touchStartY.value < currentY) {
    moveUp()
  } else {
    moveDown()
  }
  touchStartY.value = 0
  return false
}
onMounted(() => {
  inMove.value = true
  setTimeout(() => { resetAll(); calculateSectionOffsets(); scrollToSection(activeSection.value, true); inMove.value = false }, 250)
  window.addEventListener("resize", debounce(() => { resetAll(); calculateSectionOffsets(); scrollToSection(activeSection.value, true) }, 150))
  window.addEventListener("wheel", handleMouseWheel)
  window.addEventListener("touchstart", touchStart, {
    passive: false,
  }) // mobile devices
  window.addEventListener("touchmove", touchMove, {
    passive: false,
  }) // mobile devices
})
onUnmounted(() => {
  window.removeEventListener("wheel", handleMouseWheel)
  window.removeEventListener("touchstart", touchStart) // mobile devices
  window.removeEventListener("touchmove", touchMove) // mobile devices
})
</script>
<template>
  <div>
    <slot></slot>
    <Menu :items="$slots.default()" v-on:menu="scrollToSection"></Menu>
    <span fixed top-2 left-2 font-bold>Version 0.02</span>
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
