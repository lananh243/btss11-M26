<template>
  <div>
    <h3>Current Company: {{ currentCompany }}</h3>
    <h3>Age: {{ age }}</h3>
    <button @click="handleRandom">Random</button>
  </div>
</template>

<script setup>
import { onBeforeUpdate, onUpdated, ref } from "vue";
const age = ref(1);
const companies = ["Rikkei Academy", "Rikkei Education", "Rikkei Fukuoka"];
const currentCompany = ref(companies[0]);

const handleRandom = () => {
  const randomIndex = Math.floor(Math.random() * companies.length);
  currentCompany.value = companies[randomIndex];

  age.value = Math.ceil(Math.random() * 10);
};
onBeforeUpdate(() => {});
onUpdated(() => {
  console.log("Giá trị được thay đổi thành công");
});
</script>

<style scoped>
button {
  width: 90px;
  height: 35px;
  background-color: blue;
  color: white;
  border: none;
  border-radius: 5px;
}
</style>
