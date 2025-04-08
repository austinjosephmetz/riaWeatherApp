<template>
  <div class="space-y-4">
    <h3 class="text-2xl font-semibold text-gray-800">Next 24 Hours</h3>
    <div class="flex space-x-6 overflow-x-auto pb-4">
      <div v-for="hour in forecast" :key="hour.time" class="flex flex-col items-center min-w-[80px]">
        <div class="text-gray-600">{{ hour.time }}</div>
        <img :src="getWeatherIcon(hour.icon)" alt="Weather icon" class="w-12 h-12 my-2">
        <div class="text-lg font-medium text-gray-800">{{ hour.temperature }}°C</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HourlyForecast',
  props: {
    forecast: {
      type: Array,
      required: true
    }
  },
  methods: {
    getWeatherIcon(iconCode) {
      return `https://openweathermap.org/img/wn/${iconCode}@2x.png`
    }
  }
}
</script>

<style scoped>
</style> 