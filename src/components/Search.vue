<template>
  <div class="wrapper>">
    <div class="search">
      <input v-model="searchCity" class="search-input" type="text" placeholder="City" @input="toogleInput">
      <div class="weather-results" v-if="loading">
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
      loading: false,
      TOKEN: '8d410a8f575db366b3ee6cf4861281ac',
      URL_API: 'https://api.openweathermap.org/data/2.5/weather'

    }
  },
  methods: {
    toogleInput: lodash.debounce(function() {
      axios.get(`${this.URL_API}?q=${this.searchCity}&units=metric&appid=${this.TOKEN}`)
        .then((response) => {
          this.city = response.data.name
          this.temp = response.data.main.temp
          this.tempMax = response.data.main.temp_max
          this.tempMin = response.data.main.temp_min
          this.feelsLike = response.data.main.feels_like
          this.pressure = response.data.main.pressure
          this.country = response.data.sys.country

          this.loading = true
        })
        .catch((e) => {
          this.loading = false
          console.error(e)
        })
    }, 500)
  }
}

</script>
<style scoped>
p {
  font-size: large;
}
.wrapper,
.search {
  margin-top: 10vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.search-input {
  width: 200px;
  height: 30px;
  border: solid;
  border-radius: 10px 0 10px 0;
  border-width: 2px;
  padding-left: 8px;
  font-size: medium;
}

.search-input:focus {
  transition-duration: 500ms;
  border-radius: 0 10px 0 10px;
}

</style>
