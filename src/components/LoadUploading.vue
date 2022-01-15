<template>
  <div
    class="max-w-sm w-full p-5 rounded-xl bg-white shadow-lg md:p-8"
  >
  <h1 class="mb-3 text-xl">Uploading...</h1>
  <div class="rounded-lg bg-slate-50 w-full h-2 overflow-hidden">
    <div class="w-1/3 h-full rounded-lg bg-blue-600 animation-load"></div>
  </div>
  </div>
</template>

<style scoped>
.animation-load {
  animation: loading 2.5s linear infinite;
}

@keyframes loading {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(300%);
  }
}
</style>