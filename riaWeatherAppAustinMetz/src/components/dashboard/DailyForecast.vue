<template>
  <div class="space-y-4">
    <h3 class="text-2xl font-semibold text-gray-800 border-b-1 border-b-gray-200 pb-2">Next 5 Days</h3>
    <div class="flex flex-col space-x-6 overflow-x-auto pb-4 ">
      <div v-for="day in forecast" :key="day.date" class="flex items-center justify-between min-w-[100px] border-b-1 border-b-gray-200">
        <img :src="getWeatherIcon(day.icon)" alt="Weather icon" class="w-12 h-12 my-2">
        <div class="text-gray-600 font-medium">{{ day.day }}</div>
        <div class="flex gap-x-4 mt-2 px-2">
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