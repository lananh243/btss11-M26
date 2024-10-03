<template>
  <div>
    <h3>Component cha</h3>
    <Bai5Children v-if="isShow"></Bai5Children>
    <button @click="handleChange">Toggle</button>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onUnmounted, ref } from "vue";
import Bai5Children from "./Bai5Children.vue";
const isShow = ref(false);
const handleChange = () => {
  isShow.value = !isShow.value;
};
</script>

<style></style>
