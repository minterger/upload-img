<script setup>
import { inject, ref } from "@vue/runtime-core";

const uploadState = inject("uploadState");
const alert = inject("alert");

const dataImg = inject("dataImg");

const inputRef = ref(null);

const copyButton = () => {
  inputRef.value.select();
  document.execCommand("copy");
  alert.value = {
    ok: true,
    boxIcon: "clipboard",
    message: "Link copied to clipboard",
  };
};
</script>

<template>
  <div
    class="max-w-sm w-full p-5 rounded-xl bg-white shadow-lg flex items-center flex-col md:p-8"
  >
    <box-icon
      name="check-circle"
      type="solid"
      color="#219653"
      size="lg"
    ></box-icon>
    <h1 class="text-xl mt-2 mb-2">Upload Successfully!</h1>
    <img
      class="rounded-xl w-full h-52 flex items-center flex-col mt-4 bg-slate-50 object-cover hover:object-contain"
      :src="dataImg.data.secure_url"
    />
    <label class="w-full mt-5 relative">
      <button
        class="text-sm text-white rounded-lg bg-blue-600 hover:bg-blue-500 transition-colors px-3 h-9 absolute right-0.5 top-0.5 bottom-0.5"
        @click="copyButton"
      >
        Copy Link
      </button>
      <input
        type="text"
        class="rounded-lg border border-slate-300 w-full h-10 pl-2 text-xs text-slate-700 focus:outline-blue-500"
        :value="dataImg.data.url"
        ref="inputRef"
        readonly
      />
    </label>
    <button
      @click="uploadState = 'init'"
      class="rounded-xl bg-blue-600 hover:bg-blue-500 text-white py-2 px-3 fixed right-2 top-2 transition-color duration-200"
    >
      Upload other
    </button>
  </div>
</template>
