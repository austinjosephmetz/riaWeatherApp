<template>
  <div class="flex space-x-4 bg-gray-100">
    <button 
      v-for="city in cities" 
      :key="city.name"
      :class="[
        'px-6 py-3 rounded-lg transition-colors duration-200',
        selectedCity === city.name 
          ? 'bg-gray-200 text-black font-[1000]' 
          : 'bg-gray-200 text-gray-700 hover:bg-gray-300'
      ]"
      @click="$emit('city-selected', city.name)"
    >
      {{ city.name }}
    </button>
  </div>
</template>

<script>
export default {
  name: 'CityTabs',
  props: {
    cities: {
      type: Array,
      required: true
    },
    selectedCity: {
      type: String,
      required: true
    }
  }
}
</script>

<style scoped>

</style> 