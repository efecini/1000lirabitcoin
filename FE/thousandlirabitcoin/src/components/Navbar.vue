<script setup>
import { ref } from 'vue';
const navOpen = ref(false);
</script>

<template>
  <div>
    <!--- Mobile -->
    <div class="sm:hidden px-4 py-2 bg-indigo-500">
      <div>
        <button @click="navOpen = !navOpen">
          <svg
            :class="navOpen ? 'hidden' : ''"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="size-6 text-white"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M3.75 9h16.5m-16.5 6.75h16.5"
            />
          </svg>
          <svg
            :class="navOpen ? '' : 'hidden'"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="size-6 text-white"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M6 18 18 6M6 6l12 12"
            />
          </svg>
        </button>
      </div>

      <nav :class="navOpen ? '' : 'hidden'" class="text-white text-center">
        <a href="#" class="block font-bold">Logo</a>
        <a href="#" class="block">Link 1</a>
        <a href="#" class="block">Link 2</a>
        <a href="#" class="block">Link 3</a>
      </nav>
    </div>

    <!-- Desktop -->
    <div class="px-4 py-2 bg-indigo-500 hidden sm:block">
      <div class="flex gap-x-4 text-white">
        <a href="#" class="block font-bold">Logo</a>
        <a href="#" class="block">Link 1</a>
        <a href="#" class="block">Link 2</a>
        <a href="#" class="block">Link 3</a>
      </div>
    </div>
  </div>
</template>
