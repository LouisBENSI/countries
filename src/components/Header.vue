<template>
  <header class="py-4 px-2 border-b border-solid border-gray-100 shadow-sm sm:px-4 lg:px-0 dark:bg-gray-800 dark:text-white">
    <nav class="max-w-[1280px] w-full mx-auto flex items-center justify-between">
      <p class="font-extrabold text-sm">
        Where in the world ?
      </p>

      <button type="button" class="flex" @click="toggleDarkMode()">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"/>
        </svg>
        <span class="font-semibold">Dark Mode</span>
      </button>
    </nav>
  </header>
</template>


<script>
export default {
  name: 'Header',
  methods: {
    toggleDarkMode() {
      document.querySelector("html").classList.toggle("dark");
    }
  }
}
</script>


<style>
.dark>body{
  background-color: #1F2937;
}
</style>