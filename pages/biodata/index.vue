<template>
  <div class="container">
    <h1 class="title">Daftar Pengguna</h1>
    <ul class="user-list">
      <li v-for="user in users" :key="user.id" class="user-item">
        <nuxt-link :to="`/biodata/profile/${user.id}`">
          <div class="user-info">
            <h2>{{ user.name }}</h2>
            <p>{{ user.email }}</p>
          </div>
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

interface User {
  id: number;
  name: string;
  email: string;
}

const users = ref<User[]>([]);

onMounted(async () => {
  const response = await fetch(
    'https://jsonplaceholder.typicode.com/users?_limit=10'
  );
  const data = await response.json();
  users.value = data;
});
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
}

.title {
  font-size: 2rem;
  margin-bottom: 20px;
  color: #333;
}

.user-list {
  list-style-type: none;
  padding: 0;
}

.user-item {
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.user-item:hover {
  background-color: #f0f0f0;
}

.user-info {
  cursor: pointer;
}

.user-info h2 {
  margin: 0;
  font-size: 1.5rem;
}

.user-info p {
  margin: 5px 0 0;
  color: #666;
}
</style>
