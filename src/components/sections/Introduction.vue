<script setup>
import { computed } from 'vue'
import { useGlobalState } from '@/store'
const state = useGlobalState()
const effectOn = computed(() => state.value)
</script>
<template>
  <div h-full flex text-center>
    <div ma px-2 text="right 5xl" :class="{ glow: effectOn }">
      <p :class="{ 'animate-bounce': effectOn }">
        Hi, I am
        <span whitespace-nowrap>Ka Pui</span> /
        <span whitespace-nowrap>KP</span> Wong
      </p>
      <p>a Developer</p>
    </div>
    <div absolute right-1 bottom-0 flex content-end overflow-hidden class="h-40vh max-h-20vh sm:max-h-40vh">
      <img
        class="greeting-boy h-full animate-spin"
        :class="{ 'animate-0.2s': effectOn }"
        src="@/assets/byebye_boy.png"
        alt="Greeting Boy"
      />
    </div>
  </div>
</template>
<style lang="scss" scoped>
@keyframes greeting {
  from {
    transform: rotate(-10deg);
  }
  50% {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(10deg);
  }
}
.greeting-boy {
  animation-name: greeting;
  animation-direction: alternate;
}

.glow {
  animation: glow 1s ease-in-out infinite alternate;
}
@keyframes glow {
  from {
    text-shadow: 0 0 10px #fff, 0 0 20px #fff, 0 0 30px #32cfff,
      0 0 40px #32cfff, 0 0 50px #32cfff, 0 0 60px #32cfff, 0 0 70px #32cfff;
  }
  to {
    text-shadow: 0 0 20px #fff, 0 0 30px #2e31ff, 0 0 40px #2e31ff,
      0 0 50px #2e31ff, 0 0 60px #2e31ff, 0 0 70px #2e31ff, 0 0 80px #2e31ff;
  }
}
</style>
