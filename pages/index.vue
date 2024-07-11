<template>
  <div class="container">
    <h1 class="title">Selamat Datang di Beranda</h1>
    <div class="links">
      <nuxt-link to="/products" class="link">Lihat Produk</nuxt-link>
      <nuxt-link to="/dailytask" class="link">Lihat Tugas Harian</nuxt-link>
      <nuxt-link to="/biodata" class="link">Lihat BioData</nuxt-link>
    </div>
  </div>
</template>

<script setup></script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

.title {
  font-size: 2.5rem;
  margin-bottom: 20px;
  color: #333;
}

.links {
  display: flex;
  justify-content: center;
}

.link {
  padding: 10px 20px;
  margin: 0 10px;
  text-decoration: none;
  background-color: #d6efd8;
  border: 1px solid #80af81;
  border-radius: 4px;
  transition: background-color 0.3s, color 0.3s;
}

.link:hover {
  background-color: #508d4e;
  transform: scale(1.05);
}

.link:active {
  background-color: #1a5319;
  transform: scale(0.95);
}
</style>
