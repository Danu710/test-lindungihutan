<template>
  <article
    class="overflow-hidden rounded-lg border border-gray-300 shadow-xl bg-white m-5">
    <img :src="photo.url" class="h-56 w-full object-cover" alt="Photo" />
    <div class="p-4 sm:p-6 flex flex-col items-center">
      <a href="#">
        <h3 class="text-lg font-medium text-black">
          {{ props.photo.id }}
        </h3>
      </a>

      <p class="m-2 line-clamp-3 text-md/relaxed text-center text-gray-900">
        {{ props.photo.title }}
      </p>

      <a
        href="#"
        class="group mt-3 inline-flex items-center gap-1.5 rounded-lg bg-gray-100 px-5 py-2 text-sm font-semibold text-gray-600 ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:mt-0 sm:w-auto">
        Find out more
        <span
          aria-hidden="true"
          class="block transition-all group-hover:ms-0.5 rtl:rotate-180">
          {{ props.photo.thumbnailUrl }}
        </span>
      </a>
    </div>
  </article>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';

// Define props for the photo data
const props = defineProps({
  photo: {
    type: Object,
    required: true,
  },
});
</script>
