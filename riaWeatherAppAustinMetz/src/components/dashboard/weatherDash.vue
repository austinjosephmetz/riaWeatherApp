<template>
  <div class="bg-blue-700 w-full">
    <div class="h-full px-4 py-8">
      <city-tabs 
        :cities="cities" 
        :selected-city="selectedCity"
        @city-selected="selectedCity = $event"
      />

      <div class="bg-white rounded-lg shadow-lg p-6 mt-4">
        <div v-if="selectedCity" class="space-y-8">
          <h2 class="text-3xl font-bold text-gray-800">{{ selectedCity }}</h2>
          
          <!-- Current Weather -->
          <div class="flex items-center space-x-6">
            <div class="flex-shrink-0">
              <img :src="getWeatherIcon(currentWeather.icon)" alt="Weather icon" class="w-24 h-24">
            </div>
            <div class="flex-grow">
              <div class="text-5xl font-bold text-gray-800">{{ currentWeather.temperature }}°C</div>
              <div class="text-xl text-gray-600 mt-2">{{ currentWeather.description }}</div>
              <div class="flex space-x-6 text-gray-500 mt-4">
                <span>Humidity: {{ currentWeather.humidity }}%</span>
                <span>Wind: {{ currentWeather.windSpeed }} km/h</span>
              </div>
            </div>
          </div>

          <hourly-forecast :forecast="hourlyForecast" />
          <daily-forecast :forecast="dailyForecast" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CityTabs from './CityTabs.vue'
import HourlyForecast from './HourlyForecast.vue'
import DailyForecast from './DailyForecast.vue'

export default {
  name: 'WeatherDashboard',
  components: {
    CityTabs,
    HourlyForecast,
    DailyForecast
  },
  data() {
    return {
      selectedCity: 'Rio De Janeiro',
      cities: [
        { name: 'Rio De Janeiro', lat: -22.9068, lon: -43.1729 },
        { name: 'Beijing', lat: 39.9042, lon: 116.4074 },
        { name: 'Los Angeles', lat: 34.0522, lon: -118.2437 }
      ],
      currentWeather: {
        temperature: 25,
        description: 'Sunny',
        icon: '01d',
        humidity: 65,
        windSpeed: 12
      },
      hourlyForecast: [
        { time: 'Now', temperature: 25, icon: '01d' },
        { time: '12:00', temperature: 26, icon: '01d' },
        { time: '15:00', temperature: 27, icon: '01d' },
        { time: '18:00', temperature: 24, icon: '01n' },
        { time: '21:00', temperature: 22, icon: '01n' }
      ],
      dailyForecast: [
        { day: 'Mon', maxTemp: 28, minTemp: 22, icon: '01d' },
        { day: 'Tue', maxTemp: 27, minTemp: 21, icon: '02d' },
        { day: 'Wed', maxTemp: 26, minTemp: 20, icon: '03d' },
        { day: 'Thu', maxTemp: 25, minTemp: 19, icon: '04d' },
        { day: 'Fri', maxTemp: 24, minTemp: 18, icon: '09d' }
      ]
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
