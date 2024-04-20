<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <h1>Weather App</h1>
    <form @submit.prevent="getWeather">
      <input type="text" v-model="city" placeholder="Enter city name" required>
      <button type="submit">Get Weather</button>
    </form>

    <div v-if="weatherData">
      <table>
        <thead>
          <tr>
            <th>Temperature (°C)</th>
            <th>Wind Speed (m/s)</th>
            <th>Feels Like (°C)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>{{ weatherData.main.temp }}</td>
            <td>{{ weatherData.wind.speed }}</td>
            <td>{{ weatherData.main.feels_like }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      city: '',
      weatherData: null
    };
  },
  methods: {
    async getWeather() {
      try {
        const apiKey = 'e4fadba7523d71bbc75988bab9e3ff38';
        const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${apiKey}&units=metric`;
        const response = await fetch(apiUrl);
        const data = await response.json();
        this.weatherData = data;
      } catch (error) {
        console.error('Error fetching weather data:', error);
      }
    }
  }
};
</script>

<style>
/* Add your CSS styles here */
</style>
