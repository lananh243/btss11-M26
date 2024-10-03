<template>
  <div>
    <h3>Count : {{ count }}</h3>
    <button @click="handleCount">Increment</button>
  </div>
</template>

<script setup>
import { onBeforeUpdate, ref } from "vue";

const count = ref(0);
const handleCount = () => {
  count.value++;
};
onBeforeUpdate(() => {
  document.title = count.value;
});
</script>

<style></style>
