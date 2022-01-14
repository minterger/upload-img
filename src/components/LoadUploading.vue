<template>
  <div
    class="max-w-sm w-full p-5 rounded-lg bg-white shadow-lg md:p-8"
  >
  <h1 class="mt-3 mb-3 text-xl">Uploading...</h1>
  <div class="rounded-lg bg-slate-50 w-full h-2 overflow-hidden">
    <div class="w-20 h-full rounded-lg bg-blue-600 animation-load"></div>
  </div>
  </div>
</template>

<style scoped>
.animation-load {
  animation: loading 2.5s linear infinite;
}

@keyframes loading {
  0% {
    transform: translateX(-5rem);
  }
  100% {
    transform: translateX(500%);
  }
}
</style>