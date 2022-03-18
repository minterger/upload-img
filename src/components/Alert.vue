<script setup>
import { inject, onUnmounted } from "@vue/runtime-core";

const alert = inject("alert");

let timeout = setTimeout(() => {
  alert.value = null;
}, 3000);

onUnmounted(() => {
  clearTimeout(timeout);
});
</script>

<template>
  <div
    class="fixed shadow-lg bg-white rounded-xl flex items-center h-16 px-5 top-5 z-50"
  >
    <box-icon
      name="error"
      type="solid"
      color="#d00000"
      v-if="!alert.ok"
    ></box-icon>
    <box-icon
      :name="alert.boxIcon"
      type="solid"
      color="#219653"
      v-if="alert.ok"
    ></box-icon>
    <span class="ml-2">{{ alert.message }}</span>
  </div>
</template>
