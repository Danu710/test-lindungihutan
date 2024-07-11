<template>
  <div>
    <h1>Detail Pengguna</h1>
    <UserDetails v-if="user" :user="user" />
    <p v-else>Loading...</p>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import UserDetails from '~/components/UserDetails.vue';

interface User {
  name: string;
  email: string;
  phone: string;
  website: string;
  address: {
    street: string;
    suite: string;
    city: string;
    zipcode: string;
    geo: {
      lat: string;
      lng: string;
    };
  };
  company: {
    name: string;
    catchPhrase: string;
    bs: string;
  };
}

const user = ref<User | null>(null);
const route = useRoute();

console.log('user', user);

onMounted(async () => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/users/${route.params.id}`
  );
  user.value = await response.json();
});
</script>

<style scoped></style>
