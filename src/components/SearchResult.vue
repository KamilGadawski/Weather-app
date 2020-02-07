<template>
  <div>
    <h2>City: {{ weather.name }} {{ weather.sys.country }}</h2>
    <p>Temperature: {{ Math.round(weather.main.temp) }} *C</p>
    <p>Temperature min.: {{ Math.round(weather.main.temp_min) }} *C</p>
    <p>Temperature max.: {{ Math.round(weather.main.temp_max) }} *C</p>
    <p>Temperature feels: {{ Math.round(weather.main.feels_like) }} *C</p>
    <p>Pressure: {{ weather.main.pressure }} hPa</p>
  </div>
</template>
<script>
export default {
  props: {
    weather: {
      type: Object,
      require: true
    }
  }
}

</script>
<style scoped>
</style>
