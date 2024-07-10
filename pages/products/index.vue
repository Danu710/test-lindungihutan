<template>
  <div class="flex flex-row justify-between items-center m-5 p-5">
    <div class="flex justify-start items-center">
      <h1 class="text-2xl font-mono text-black shadow-md">Pages Photos</h1>
    </div>
    <div class="flex justify-end items-center">
      <div class="relative">
        <label for="Search" class="sr-only"> Search </label>

        <input
          type="text"
          id="Search"
          v-model="searchQuery"
          placeholder="Search title photo..."
          class="w-full rounded-md border-gray-200 py-2.5 pe-10 shadow-sm sm:text-sm p-5" />

        <span class="absolute inset-y-0 end-0 grid w-10 place-content-center">
          <button type="button" class="text-gray-600 hover:text-gray-700">
            <span class="sr-only">Search</span>

            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="h-4 w-4">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
            </svg>
          </button>
        </span>
      </div>
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
</script>
