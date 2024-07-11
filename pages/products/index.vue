<template>
  <div class="flex flex-col items-center justify-center p-5 m-5">
    <BackButton />
    <div class="flex flex-row justify-between gap-10">
      <h1
        class="p-2 font-mono text-2xl text-black border-gray-300 shadow-sm border-y">
        Pages Photos
      </h1>

      <SearchInput
        :searchQuery="searchQuery"
        @update:searchQuery="updateSearchQuery" />
    </div>

    <div
      class="grid justify-center grid-cols-1 gap-1 m-5 md:grid-cols-3 md:gap-3">
      <PhotoCard
        v-for="photo in filteredPhotos"
        :key="photo.id"
        :photo="photo" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';

interface Photo {
  albumId: number;
  id: number;
  title: string;
  url: string;
  thumbnailUrl: string;
}

const photos = ref<Photo[]>([]);
const searchQuery = ref('');

const fetchPhotos = async () => {
  const response = await fetch(
    'https://jsonplaceholder.typicode.com/photos?_limit=10',
    {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      },
    }
  );

  photos.value = await response.json();
};

onMounted(() => {
  fetchPhotos();
});

const filteredPhotos = computed(() => {
  if (!searchQuery.value) {
    return photos.value;
  }

  const query = searchQuery.value.toLowerCase();
  return photos.value.filter((photo: any) =>
    photo.title.toLowerCase().includes(query)
  );
});

const updateSearchQuery = (value: string) => {
  searchQuery.value = value;
};
</script>
