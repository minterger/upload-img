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
  <div class="fixed shadow-lg bg-white rounded-xl flex items-center h-16 px-5 top-5">
    <box-icon name='error' type='solid' color='#d00000' v-show="!alert.ok"></box-icon><span class="ml-2">{{alert.message}}</span>
  </div>
</template>