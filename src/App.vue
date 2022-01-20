<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
// https://codepen.io/WebDEasy/pen/NVOEBL but in vue 3 things
import 'normalize.css'
import 'uno.css'

import Construction from '@/components/Contructing.vue'
import Section from '@/components/Section.vue'
import FullPageScroll from './components/FullPageScroll.vue';
</script>

<template>
  <div id="app">
    <FullPageScroll>
      <Section class="blue">
        <Construction />
      </Section>
      <Section class="black">
        <h1>Section 2</h1>
      </Section>
      <Section class="green">
        <h1>Section 3</h1>
      </Section>
      <Section class="blue">
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
