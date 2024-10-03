<template>
  <div>
    <h3>Age : {{ count }}</h3>
    <button @click="handleCount">Increase age</button>
    <Bai4Children :countProps="count"></Bai4Children>
  </div>
</template>

<script setup>
import Bai4Children from "./Bai4Children.vue";
import { ref } from "vue";
const count = ref(0);
const handleCount = () => {
  count.value++;
};
</script>

<style></style>
