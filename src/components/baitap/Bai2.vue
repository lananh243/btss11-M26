<template>
  <div>
    <h3>Counter : {{ count }}</h3>
    <button @click="handleCount">Counter</button>
  </div>
</template>

<script setup>
import { onBeforeMount, onBeforeUpdate, onMounted, onUpdated, ref } from "vue";

const count = ref(0);
const handleCount = () => {
  count.value++;
};
onBeforeMount(() => {});
onMounted(() => {});
onBeforeUpdate(() => {});
onUpdated(() => {
  console.log("Dữ liệu đã thay đổi");
});
</script>

<style></style>
