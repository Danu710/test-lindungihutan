<template>
  <div v-if="user" class="user-details">
    <div class="header">
      <img
        class="avatar"
        :src="'https://i.pravatar.cc/150?img=' + user.id"
        alt="User Avatar" />
      <h2>{{ user.name }}</h2>
      <p class="email">{{ user.email }}</p>
    </div>
    <div class="info">
      <div class="section">
        <h3>Contact Information</h3>
        <p><strong>Phone:</strong> {{ user.phone }}</p>
        <p>
          <strong>Website:</strong>
          <a :href="`http://${user.website}`" target="_blank">{{
            user.website
          }}</a>
        </p>
      </div>
      <div class="section">
        <h3>Address</h3>
        <p>{{ user.address.street }}</p>
        <p>{{ user.address.suite }}</p>
        <p>{{ user.address.city }}</p>
        <p>{{ user.address.zipcode }}</p>
        <p>{{ user.address.geo.lat }}, {{ user.address.geo.lng }}</p>
      </div>
      <div class="section">
        <h3>Company</h3>
        <p><strong>Name:</strong> {{ user.company.name }}</p>
        <p><strong>Catch Phrase:</strong> {{ user.company.catchPhrase }}</p>
        <p><strong>Business:</strong> {{ user.company.bs }}</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
interface User {
  id: number;
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

const props = defineProps<{
  user: User;
}>();
</script>

<style scoped>
.user-details {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

.header {
  display: flex;
  align-items: center;
  gap: 20px;
  border-bottom: 1px solid #eaeaea;
  padding-bottom: 20px;
  margin-bottom: 20px;
}

.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid #ccc;
}

.header h2 {
  margin: 0;
}

.email {
  color: #555;
  font-size: 14px;
}

.info {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.section {
  background-color: #fff;
  padding: 15px;
  border-radius: 4px;
  border: 1px solid #eaeaea;
}

.section h3 {
  margin-top: 0;
  margin-bottom: 10px;
  font-size: 18px;
  border-bottom: 1px solid #eaeaea;
  padding-bottom: 5px;
}

.section p {
  margin: 5px 0;
}

a {
  color: #007bff;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>
