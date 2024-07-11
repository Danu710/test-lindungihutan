<template>
  <div v-if="user" class="user-details">
    <h2>{{ props.user.name }}</h2>
    <p><strong>Email:</strong> {{ props.user.email }}</p>
    <p><strong>Phone:</strong> {{ props.user.phone }}</p>
    <p>
      <strong>Website:</strong>
      <a :href="`http://${user.website}`" target="_blank">{{
        props.user.website
      }}</a>
    </p>
    <div>
      <strong>Address</strong>
      <p>{{ props.user.address.street }}</p>
      <p>{{ props.user.address.suite }}</p>
      <p>{{ props.user.address.city }}</p>
      <p>{{ props.user.address.zipcode }}</p>
      <p>{{ props.user.address.geo.lat }}, {{ props.user.address.geo.lng }}</p>
    </div>
    <div>
      <strong>Company</strong>
      <p>{{ props.user.company.name }}</p>
      <p>{{ props.user.company.catchPhrase }}</p>
      <p>{{ props.user.company.bs }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
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

const props = defineProps<{
  user: User;
}>();
</script>

<style scoped>
.user-details {
  border: 1px solid #ddd;
  padding: 16px;
  border-radius: 4px;
  margin-top: 24px;
}

h2 {
  font-size: 24px;
  margin-bottom: 16px;
}

p {
  margin: 8px 0;
}

a {
  color: #007bff;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>
