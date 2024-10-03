<template></template>

<script setup>
import { onBeforeUpdate, onUpdated } from "vue";

const props = defineProps(["countProps"]);

onBeforeUpdate(() => {});
onUpdated(() => {
  alert("Giá trị của biến age đã thay đổi");
});
</script>

<style></style>
