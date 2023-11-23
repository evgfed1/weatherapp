<template>

  <div class='wrapper'>

    <h1>Weather App </h1>
    <p>Weather in {{ city == "" ? ' your town' : cityName }}</p>
    <input type='text' v-model='city' placeholder='Text here'>
    <button v-if='city != "" ' type='button' class="btn btn-outline-primary" @click='getWeather()'>Get weather</button>
    <p class='error'>{{ errorMessage }}</p>
    <p v-show="info != null">Temperature is  °C</p>
    <p v-show="info != null">Pressure is Pa</p>

  </div>

</template>


<script>
import axios from "axios";

export default {
  data() {
    return {
      city: '',
      errorMessage: '',
      info: null

    }
  },
  computed: {
    cityName() {
      return '«' + this.city + '»'
    }
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2 || this.city.trim().length > 30) {
        this.handleCityNameFieldAlert()
        return false
      }
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&lon=-2.15&appid=49dfee298069d09bd1fb86eaa4f84fd0&units=metric`)
          .then(result => (this.info = result.data))
    },
    handleCityNameFieldAlert() {
      this.errorMessage = 'City name is incorrect'
      setTimeout(this.resetErrorMessage, 2000)
    },

    resetErrorMessage() {
      this.errorMessage = ''
    }
  }
}
</script>


