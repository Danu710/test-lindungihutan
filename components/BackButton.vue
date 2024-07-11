<template>
  <button @click="goBack" class="back-button">Back To Home</button>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router';

const router = useRouter();

const goBack = () => {
  router.push('/');
};
</script>

<style scoped>
.back-button {
  position: fixed;
  top: 20px;
  left: 20px;
  background-color: #77e4c8;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  font-size: 16px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease, transform 0.3s ease;
  z-index: 1000;
}

.back-button:hover {
  background-color: #36c2ce;
  transform: scale(1.05);
}

.back-button:active {
  background-color: #478ccf;
  transform: scale(0.95);
}
</style>
