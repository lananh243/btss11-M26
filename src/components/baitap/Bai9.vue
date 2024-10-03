<template>
  <div>
    <h3>Ứng dụng đếm số</h3>
    <p>Count {{ count }}</p>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";

const count = ref(0);
let countId;
onMounted(() => {
  countId = setInterval(() => {
    count.value++;
  }, 1000);
});
onBeforeUnmount(() => {
  clearInterval(countId);
});
</script>

<style></style>
