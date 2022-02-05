<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
// https://codepen.io/WebDEasy/pen/NVOEBL but in vue 3 things
import 'normalize.css'
import 'uno.css'

import Section from './components/Section.vue'
import FullPageScroll from './components/FullPageScroll.vue'
import Introduction from "./components/sections/Introduction.vue"
import WhatCanIDo from './components/sections/WhatCanIDo.vue'
</script>

<template>
  <div id="app">
    <FullPageScroll>
      <Section display="Introduction" class="blue">
        <Introduction />
      </Section>
      <Section multi-page display="What I Can Do" class="black h-200vh">
        <WhatCanIDo />
      </Section>
      <Section display="What I Can't Do" class="green">
        <h1>What I Can't Do</h1>
      </Section>
      <Section display="(No) Showcase" class="blue">
        <h1>(No) Showcase</h1>
      </Section>
      <Section display="Contact" class="blue">
        <h1>Contact</h1>
      </Section>
      <Section display="Hobbies" class="blue">
        <h1>Hobbies</h1>
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
