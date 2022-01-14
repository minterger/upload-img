<script setup>
import { ref } from "@vue/reactivity";
import { onMounted } from "@vue/runtime-core";

const dropzoneIsActive = ref(false);
const file = ref(null);

const toggleDrag = () => {
  if (!file.value) dropzoneIsActive.value = !dropzoneIsActive.value;
};

const uploadImg = (e) => {
  file.value = e.value.files[0];
  console.log(file.value);
};

const dropFile = (e) => {
  file.value = e.dataTransfer.files[0];
  console.log(file.value);
};
</script>

<template>
  <div
    class="max-w-sm w-full p-5 rounded-lg bg-white shadow-lg flex items-center flex-col md:p-8"
  >
    <h1 class="mt-3 mb-3 text-2xl">Upload your image</h1>
    <span class="text-xs mt-2 mb-2 text-slate-600"
      >File should be Jpeg, Png,...</span
    >
    <div
      @dragenter.prevent="toggleDrag"
      @dragleave.prevent="toggleDrag"
      @dragover.prevent=""
      @drop.prevent="dropFile"
      class="border border-blue-500 border-dashed rounded-lg w-full h-52 flex items-center flex-col mt-4 bg-slate-50 transition-all duration-200"
      :class="{
        'bg-blue-500 border-solid': dropzoneIsActive,
      }"
    >
      <img src="../assets/image.svg" class="mt-7 mb-7" alt="" />
      <span
        class="text-sm text-slate-500 mb-7 transition-text duration-200"
        :class="{ 'text-white': dropzoneIsActive }"
      >
        Drag & Drop your image here</span
      >
    </div>

    <span class="text-sm text-slate-500 mt-4 mb-4">Or</span>
    <label
      for="file"
      class="py-1 px-3 rounded-lg text-white bg-blue-600 hover:bg-blue-500 transition-colors shadow"
    >
      Choose a File
      <input
        type="file"
        class="hidden"
        id="file"
        @change="uploadImg"
      />
    </label>
  </div>
</template>
