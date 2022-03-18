<script setup>
import axios from "axios";
import { ref } from "@vue/reactivity";
import { inject } from "@vue/runtime-core";

const uploadState = inject("uploadState");
const dataImg = inject("dataImg");
const alert = inject("alert");

const isDropzoneActive = ref(false);
const file = ref(null);

const toggleDrag = () => {
  if (!file.value) isDropzoneActive.value = !isDropzoneActive.value;
};

const uploadButtonImg = (e) => {
  file.value = e.target.files[0];
  uploadImg();
};

const dropFile = (e) => {
  file.value = e.dataTransfer.files[0];
  if (file.value) {
    uploadImg();
  } else {
    isDropzoneActive.value = false;
  }
};

const uploadImg = async () => {
  const formData = new FormData();
  formData.append("image", file.value);
  uploadState.value = "upload";

  // axios
  //   .post(
  //     "https://api.imgbb.com/1/upload?key=45f666aa12a2edd235f9e6bf8378d22d",
  //     formData
  //   )

  try {
    const res = await axios.post(
      import.meta.env.VITE_URL_API + "/upload",
      formData
    );

    dataImg.value = res.data;
    uploadState.value = "end";
  } catch (error) {
    alert.value = error.response.data;
    uploadState.value = "init";
  }
};
</script>

<template>
  <div
    class="max-w-sm w-full p-5 rounded-xl bg-white shadow-lg flex items-center flex-col md:p-8"
  >
    <h1 class="mt-3 mb-3 text-xl">Upload your image</h1>
    <span class="text-xs mt-2 mb-2 text-slate-600"
      >File should be Jpeg, Png,...</span
    >
    <div
      @dragenter.prevent="toggleDrag()"
      @dragleave.prevent="toggleDrag()"
      @dragover.prevent=""
      @drop.prevent="dropFile"
      class="border-blue-500 border-2 rounded-xl w-full h-52 flex items-center flex-col mt-4 transition-all duration-200"
      :class="[
        isDropzoneActive ? 'border bg-blue-500' : 'border-dashed bg-slate-50',
      ]"
    >
      <img src="../assets/image.svg" class="mt-7 mb-7" alt="" />
      <span
        class="text-sm mb-7 transition-text duration-200"
        :class="[isDropzoneActive ? 'text-white' : 'text-slate-600']"
      >
        Drag & Drop your image here</span
      >
    </div>

    <span class="text-sm text-slate-500 mt-4 mb-4">Or</span>
    <label
      for="file"
      class="px-3 py-2 text-sm text-white rounded-lg bg-blue-600 hover:bg-blue-500 transition-colors shadow"
    >
      Choose a File
      <input
        type="file"
        class="hidden"
        id="file"
        @change.prevent="uploadButtonImg"
      />
    </label>
  </div>
</template>
