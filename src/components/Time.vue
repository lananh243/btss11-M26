<template>
  <div>
    <h1>Time : {{ time }}</h1>
  </div>
</template>

<script setup>
import {
  onBeforeMount,
  onBeforeUnmount,
  onBeforeUpdate,
  onMounted,
  onUnmounted,
  onUpdated,
  ref,
} from "vue";

const time = ref(0);
let timerId;
// Giai đoạn Mounting
onBeforeMount(() => {
  console.log("Component before mount");
});

onMounted(() => {
  timerId = setInterval(() => {
    time.value++;
  }, 1000);
  console.log("Component Mounted");
});
// Giai đoạn Updating
onBeforeUpdate(() => {
  console.log("Component before Update");
});

onUpdated(() => {
  console.log("Component Updated");
});

// Giai đoạn unMount
onBeforeUnmount(() => {
  console.log("Component before Unmount");
  clearInterval(timerId);
});
onUnmounted(() => {
  console.log("component unmounted");
});
</script>

<style></style>
