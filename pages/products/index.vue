<template>
  <div class="flex flex-row justify-between items-center m-5 p-5">
    <div class="flex justify-start items-center">
      <h1 class="text-2xl font-mono text-black shadow-md">Pages Photos</h1>
    </div>
    <div class="flex justify-end items-center">
      <SearchInput
        :searchQuery="searchQuery"
        @update:searchQuery="updateSearchQuery" />
    </div>
  </div>

  <div class="grid grid-cols-3 justify-center gap-3 m-5">
    <PhotoCard v-for="photo in filteredPhotos" :key="photo.id" :photo="photo" />
  </div>
</template>

<script setup lang="ts">
const searchQuery = ref('');

const { data: photos } = await useFetch(
  'https://jsonplaceholder.typicode.com/photos',
  {
    params: {
      _limit: 10,
    },
    transform: (photos: any) =>
      photos.map((product: any) => ({
        title: product.title,
        id: product.id,
        url: product.url,
        thumbnailUrl: product.thumbnailUrl,
      })),
  }
);

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
