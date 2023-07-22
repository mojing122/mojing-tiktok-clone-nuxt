<template>
  <div class="w-[100%] relative flex justify-center">
    <div
      class="absolute top-6 z-50 mx-auto bg-black bg-opacity-70 text-white px-14 py-3 rounded-sm"
      :class="errorType ? 'visible' : 'invisible'"
    >
      {{ error }}
    </div>
  </div>
</template>

<script setup>
const props = defineProps(["errorType"]);
const { errorType } = toRefs(props);

let error = ref("");

watch(
  () => errorType.value,
  () => {
    if (errorType.value == "caption") {
      error.value = "视频标题不能多于150字符";
    } else if (errorType.value == "bio") {
      error.value = "视频标题不能多于80字符";
    } else if (errorType.value == "file") {
      error.value = "视频上传失败，请使用MP4格式";
    } else {
      error.value = "";
    }
  }
);
</script>
