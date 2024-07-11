<template>
  <article
    class="m-5 overflow-hidden bg-white border border-gray-300 rounded-lg shadow-xl">
    <img :src="photo.url" class="object-cover w-full h-56" alt="Photo" />
    <div class="flex flex-col items-center p-4 sm:p-6">
      <a href="#">
        <h3 class="text-lg font-medium text-black">
          {{ props.photo.id }}
        </h3>
      </a>

      <p class="m-2 text-center text-gray-900 line-clamp-3 text-md/relaxed">
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
interface Photo {
  id: number;
  title: string;
  url: string;
  thumbnailUrl: string;
}

const props = defineProps<{ photo: Photo }>();
</script>
