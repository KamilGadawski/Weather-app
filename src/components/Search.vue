<template>
  <div class="wrapper>">
    <div class="search">
      <label>Search</label>
      <input v-model="searchCity" type="text" placeholder="City" @input="toogleInput">
      <div class="weather-results">
        <h2>City: {{ city }} {{ country }}</h2>
        <p>Temperature: {{ Math.round(temp) }} *C</p>
        <p>Temperature min.: {{ Math.round(tempMin) }} *C</p>
        <p>Temperature max.: {{ Math.round(tempMax) }} *C</p>
        <p>Temperature feels: {{ Math.round(feelsLike) }} *C</p>
        <p>Pressure: {{ pressure }} hPa</p>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import lodash from 'lodash'

export default {
  name: 'Search',
  data() {
    return {
      searchCity: '',
      city: '',
      temp: '',
      feelsLike: '',
      tempMin: '',
      tempMax: '',
      pressure: '',
      country: '',
      TOKEN: '8d410a8f575db366b3ee6cf4861281ac',
      URL_API: 'https://api.openweathermap.org/data/2.5/weather'

    }
  },
  methods: {
    toogleInput: lodash.debounce(function() {
      axios.get(`${this.URL_API}?q=${this.searchCity}&units=metric&appid=${this.TOKEN}`)
        .then((response) => {
          console.log(response)
          this.city = response.data.name
          this.temp = response.data.main.temp
          this.tempMax = response.data.main.temp_max
          this.tempMin = response.data.main.temp_min
          this.feelsLike = response.data.main.feels_like
          this.pressure = response.data.main.pressure
          this.country = response.data.sys.country
        })
        .catch((e) => {
          console.error(e)
        })
    }, 500)
  }
}

</script>
<style scoped>
.wrapper,
.search {
  display: flex;
  flex-direction: column;
  align-items: center;
}

</style>
