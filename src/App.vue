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
import WhatICantDo from './components/sections/WhatICantDo.vue'
import NoShowcase from './components/sections/NoShowcase.vue'
import Contact from './components/sections/Contact.vue'
import Hobbies from './components/sections/Hobbies.vue'
</script>

<template>
  <FullPageScroll>
    <Section ref="el" display="Introduction" class="blue">
      <Introduction />
    </Section>
    <Section multi-page display="What I Can Do" class="black">
      <WhatCanIDo />
    </Section>
    <Section display="What I Can't Do" class="green">
      <WhatICantDo />
    </Section>
    <Section display="(No) Showcase" class="brown">
      <NoShowcase />
    </Section>
    <Section display="Contact" class="red">
      <Contact />
    </Section>
    <Section display="Hobbies" class="black">
      <Hobbies />
    </Section>
  </FullPageScroll>
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
