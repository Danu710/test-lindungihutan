<template>
  <div class="container">
    <h1 class="title">Beranda</h1>
    <div class="links">
      <nuxt-link to="/products" class="link">Product</nuxt-link>
      <nuxt-link to="/dailytask" class="link">Tugas Harian</nuxt-link>
      <nuxt-link to="/biodata" class="link">BioData</nuxt-link>
    </div>
  </div>
</template>

<script setup></script>

<style scoped>
.container {
  max-width: 600px;
  height: 400px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
  background-color: #f9f9f9;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.title {
  font-size: 2.5rem;
  margin-bottom: 2rem;
  color: #333;
  font-weight: bold;
}

.links {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}

.link {
  display: inline-block;
  padding: 0.75rem 1.5rem;
  font-size: 1.25rem;
  font-weight: 500;
  color: #fff;
  background-color: #007bff;
  border-radius: 4px;
  text-decoration: none;
  transition: background-color 0.3s ease;
}

.link:hover {
  background-color: #0069d9;
}
</style>
