<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
// https://codepen.io/WebDEasy/pen/NVOEBL but in vue 3 things
import 'normalize.css'
import 'uno.css'

import Section from './components/Section.vue'
import FullPageScroll from './components/FullPageScroll.vue'
import Introduction from "./components/sections/Introduction.vue"
</script>

<template>
  <div id="app">
    <FullPageScroll>
      <Section id="introduction" class="blue">
        <Introduction />
      </Section>
      <Section multi-page id="what-can-i-do" class="black h-200vh">
        <h1>Section 2</h1>
      </Section>
      <Section id="contact" class="green">
        <h1>Section 3</h1>
      </Section>
      <Section id="hobbies" class="blue">
        <h1>Section 4</h1>
      </Section>
    </FullPageScroll>
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
</style>
