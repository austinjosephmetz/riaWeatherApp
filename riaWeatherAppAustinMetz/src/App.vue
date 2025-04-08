<script setup>
import weatherDash from './components/dashboard/weatherDash.vue'
</script>

<template>
  <div class="min-h-screen w-full bg-blue-500">
    Title
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
