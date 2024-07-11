<template>
  <div class="container">
    <h1 class="title">Daftar Pengguna</h1>
    <ul class="ul">
      <li v-for="user in users" :key="user.id" class="li">
        <nuxt-link :to="`/biodata/profile/${user.id}`"
          >{{ user.name }} <br
        /></nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

interface User {
  id: number;
  name: string;
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
  max-width: 600px;
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

.ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.li {
  margin-bottom: 1rem;
}
</style>
