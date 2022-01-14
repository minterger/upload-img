<script setup>
import { provide, ref } from 'vue';
import UploadComponent from './components/UploadComponent.vue';
import LoadUploading from './components/LoadUploading.vue';
import InfoUpload from './components/InfoUpload.vue';

const isUploadActive = ref(false);
const isUploadFinished = ref(false);

const dataImg = ref({});

provide('isUploadActive', isUploadActive);
provide('isUploadFinished', isUploadFinished);
provide('dataImg', dataImg);
</script>

<template>
  <main class="min-h-screen bg-slate-50 flex justify-center items-center	px-2">
    <upload-component v-if="!isUploadActive && !isUploadFinished" />
    <load-uploading v-if="isUploadActive"/>
    <info-upload v-if="isUploadFinished"/>
  </main>
</template>