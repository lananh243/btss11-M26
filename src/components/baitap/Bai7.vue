<template>
  <div>
    <input type="text" v-model="inputValue" />
  </div>
</template>

<script setup>
import { onBeforeUpdate, ref } from "vue";

const inputValue = ref("");

onBeforeUpdate(() => {
  document.title = inputValue.value;
});
</script>

<style></style>
