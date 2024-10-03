<template>
  <div>
    <h1>Children Component</h1>
    <h2>Count : {{ count }}</h2>
    <input type="text" v-model="inputValue" />
    <button @click="handleIncrease">Count</button>
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
const count = ref(0);
const inputValue = ref("");
// Các phương thức trong giai đoạn Mounting
onBeforeMount(() => {
  console.log("Component before mount");
});

onMounted(() => {
  //   count.value = 2;
  console.log("Component mounted");
});

// Các phương thức trong giai đoạn updation
onBeforeUpdate(() => {
  document.title = inputValue.value;
  console.log("Before update");
});
const handleIncrease = () => {
  count.value++;
};
onUpdated(() => {
  inputValue.value = "Nguyễn Lan Anh";
  console.log("Component Updated");
});

// Các phương thức trong giai đoạn unMount
onBeforeUnmount(() => {
  console.log("Component Before unmount");
});

onUnmounted(() => {
  console.log("Component unMounted");
});
</script>

<style></style>
