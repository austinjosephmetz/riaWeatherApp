<template>
  <div class="bg-blue-400 w-full">
    <city-tabs 
        :cities="cities" 
        :selected-city="selectedCity"
        @city-selected="changeCity($event)"
      />
    <div class="h-full px-4 py-2">
      <div class="bg-white rounded-lg shadow-lg p-6">
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
              <div class="flex gap-x-4 text-gray-500 mt-4">
                <div>Humidity: {{ currentWeather.humidity }}%</div>
                <div>Wind: {{ currentWeather.windSpeed }} km/h</div>
              </div>
            </div>
          </div>

          
        </div>
      </div>
    </div>

    <div class="px-4 py-4"><hourly-forecast :forecast="hourlyForecast" class="bg-white rounded-lg shadow-lg p-6"/></div>
    <div class="px-4 py-4"><daily-forecast :forecast="dailyForecast" class="bg-white rounded-lg shadow-lg p-6"/></div>
  </div>
</template>

<script>
import axios from 'axios';
import _ from 'lodash';
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
  created(){
    this.changeCity('Rio De Janeiro')
  },

  methods: {
    getWeatherIcon(iconCode) {
      return `https://openweathermap.org/img/wn/${iconCode}@2x.png`
    },

    async changeCity(city){
      this.selectedCity = city
      //get the index of the city we are switching to in order to get the correct lat/long for requests
      let nextCity = _.findIndex(this.cities, (c) => {return c.name === city})
      //Likely would have the access key as an env variable on whatever is hosting the application but for now just using a static string
      //first request is current weather and second is forecast, it seems the free version doesn't include hourly forecast for today and starts its daily forecast at 12am of the following day
      let currentWeatherResponse = await axios.get(`https://api.openweathermap.org/data/2.5/weather?lat=${this.cities[nextCity].lat}&lon=${this.cities[nextCity].lon}&appid=9170e0e85794088df319259526c55afd&units=metric`)

      //update value for current weather
      this.currentWeather.temperature = currentWeatherResponse.data.main.temp
      this.currentWeather.description = currentWeatherResponse.data.weather[0].description
      this.currentWeather.icon = currentWeatherResponse.data.weather[0].icon
      this.currentWeather.humidity = currentWeatherResponse.data.main.humidity
      this.currentWeather.windSpeed = currentWeatherResponse.data.wind.speed

      //this is the free api call for 5-day / 3-hour forecast so weather every 3 hours for the next 5 days
      // let dailyForecastResponse = await axios.get(`https://api.openweathermap.org/data/2.5/forecast?lat=${this.cities[nextCity].lat}&lon=${this.cities[nextCity].lon}&appid=9170e0e85794088df319259526c55afd&units=metric`)
      // console.log(dailyForecastResponse.data)
    }
  }
}
</script>

<style scoped>
</style>
