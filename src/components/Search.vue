<template>
  <div class="wrapper>">
    <div class="search">
      <input v-model="searchCity" class="search-input" type="text" placeholder="City" @input="toogleInput">
      <div class="weather-results" v-if="loading">
        <SearchResult :weather="weather"/>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import lodash from 'lodash'
import SearchResult from '@/components/SearchResult'
export default {
  name: 'Search',
  components: {
    SearchResult
  },
  data() {
    return {
      searchCity: '',
      weather: [],
      loading: false,
      TOKEN: '8d410a8f575db366b3ee6cf4861281ac',
      URL_API: 'https://api.openweathermap.org/data/2.5/weather'

    }
  },
  methods: {
    toogleInput: lodash.debounce(function() {
      axios.get(`${this.URL_API}?q=${this.searchCity}&units=metric&appid=${this.TOKEN}`)
        .then((response) => {
          this.weather = response.data

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
