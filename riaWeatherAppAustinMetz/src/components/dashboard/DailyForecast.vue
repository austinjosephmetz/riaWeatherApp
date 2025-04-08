<template>
  <div class="space-y-4">
    <h3 class="text-2xl font-semibold text-gray-800">5-Day Forecast</h3>
    <div class="flex space-x-6 overflow-x-auto pb-4">
      <div v-for="day in forecast" :key="day.date" class="flex flex-col items-center min-w-[100px]">
        <div class="text-gray-600 font-medium">{{ day.day }}</div>
        <img :src="getWeatherIcon(day.icon)" alt="Weather icon" class="w-12 h-12 my-2">
        <div class="flex justify-between w-full mt-2">
          <span class="text-red-500 font-medium">{{ day.maxTemp }}°C</span>
          <span class="text-blue-500 font-medium">{{ day.minTemp }}°C</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DailyForecast',
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