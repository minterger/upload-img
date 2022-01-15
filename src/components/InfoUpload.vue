<script setup>
import { inject, ref } from "@vue/runtime-core";

const dataImg = inject("dataImg");

const inputRef = ref(null);

const copyButton = () => {
  inputRef.value.select();
  document.execCommand("copy");
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
      class="rounded-xl w-full h-52 flex items-center flex-col mt-4 bg-slate-50 transition-all duration-200 object-cover hover:object-contain"
      :src="dataImg.data.url"
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
        class="rounded-lg border border-slate-300 w-full h-10 pl-2 text-xs text-slate-700"
        :value="dataImg.data.url"
        ref="inputRef"
        readonly
      />
    </label>
  </div>
</template>
