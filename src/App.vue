<script setup>
import { provide, ref } from "vue";
import AlertVue from "./components/Alert.vue";
import UploadComponent from "./components/UploadComponent.vue";
import LoadUploading from "./components/LoadUploading.vue";
import InfoUpload from "./components/InfoUpload.vue";

const uploadState = ref("init");
const alert = ref(null);

const dataImg = ref({});

provide("uploadState", uploadState);
provide("dataImg", dataImg);
provide("alert", alert);
</script>

<template>
  <main class="min-h-screen bg-slate-50 flex justify-center items-center px-2">
    <transition name="fade" mode="out-in">
      <alert-vue v-if="alert" />
    </transition>
    <transition name="fade" mode="out-in">
      <upload-component v-if="uploadState === 'init'" />
      <load-uploading v-else-if="uploadState === 'upload'" />
      <info-upload v-else-if="uploadState === 'end'" />
    </transition>
  </main>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
