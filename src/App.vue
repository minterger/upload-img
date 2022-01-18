<script setup>
import { provide, ref } from 'vue';
import AlertVue from './components/Alert.vue';
import UploadComponent from './components/UploadComponent.vue';
import LoadUploading from './components/LoadUploading.vue';
import InfoUpload from './components/InfoUpload.vue';

const isUploadActive = ref(false);
const isUploadFinished = ref(false);
const alert = ref(null);

const dataImg = ref({});

provide('isUploadActive', isUploadActive);
provide('isUploadFinished', isUploadFinished);
provide('dataImg', dataImg);
provide('alert', alert);
</script>

<template>
  <main class="min-h-screen bg-slate-50 flex justify-center items-center	px-2">
    <alert-vue v-if="alert"/>
    <upload-component v-if="!isUploadActive && !isUploadFinished" />
    <load-uploading v-if="isUploadActive"/>
    <info-upload v-if="isUploadFinished"/>
  </main>
</template>