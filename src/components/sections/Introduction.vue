<template>
  <div h-full flex text-center select-none>
    <div ma text="right 5xl">
      <div>
        Hi, I am Ben Wong
      </div>
      <div>
        a Developer
      </div>
    </div>
    <div absolute right-1 bottom-0 flex content-end>
      <img animate-spin animate="count-infinite 2s" class="greeting-boy h-30% max-h-30%" src="@/assets/byebye_boy.png" alt="Greeting Boy">
    </div>
  </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>
@keyframes greeting {
  0% {transform:rotate(-10deg);}
  50% {transform:rotate(0deg);}
  100% {transform:rotate(10deg);}
}
.greeting-boy {
  animation-name: greeting;
  animation-direction: alternate;
}
</style>
