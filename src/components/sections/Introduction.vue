<template>
  <div h-full flex text-center select-none>
    <div ma text="right 5xl">
      <div>
        Hi, I am
        <span whitespace-nowrap>Ka Pui</span> /
        <span whitespace-nowrap>KP</span> Wong
      </div>
      <div>a Developer</div>
    </div>
    <div absolute right-1 bottom-0 flex content-end overflow-hidden class="h-40vh max-h-20vh sm:max-h-40vh">
      <img
        animate-spin
        animate="count-infinite 2s"
        class="greeting-boy h-full"
        src="@/assets/byebye_boy.png"
        alt="Greeting Boy"
      />
    </div>
  </div>
</template>

<script setup>

</script>

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
</style>
