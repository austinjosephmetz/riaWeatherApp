<template>
  <div class="flex space-x-4 bg-gray-100 w-full inset-shadow-sm/50 p-1">
    <button 
      v-for="city in cities" 
      :key="city.name"
      :class="[
        'px-6 py-3 transition-colors duration-200 text-2xl',
        selectedCity === city.name 
          ? 'bg-gray-100 text-black font-extrabold border-b-amber-500 border-b-2' 
          : 'bg-gray-100 text-gray-600 hover:bg-gray-300'
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