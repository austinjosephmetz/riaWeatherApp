<script setup>
import weatherDash from './components/dashboard/weatherDash.vue'
</script>

<template>
  <div class="min-h-screen w-full bg-blue-400">
    <div class="flex justify-between align-middle">
      <h1 class="text-white text-4xl font-extrabold p-6">Simple Weather</h1>
      <i class="pi pi-search text-white text-2xl pb-4 pt-8 px-6"></i>
    </div>
    <weatherDash />
  </div>
</template>

<style>
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

#app {
  width: 100%;
  height: 100%;
}
</style>
