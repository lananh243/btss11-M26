<template>
  <div>
    <h3>Chiều rộng cửa sổ: {{ windowWidth }} px</h3>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const windowWidth = ref(window.innerWidth);

const updateWindowWidth = () => {
  windowWidth.value = window.innerWidth;
};

onMounted(() => {
  window.addEventListener("resize", updateWindowWidth);
});

onBeforeUnmount(() => {
  window.removeEventListener("resize", updateWindowWidth);
});
</script>

<style scoped></style>
