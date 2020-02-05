<template>
  <div class="app">
    <Search />
  </div>
</template>
<script>
import Search from '@/components/Search'

export default {
  name: 'app',
  components: {
    Search
  }
}

</script>
<style scoped>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  box-sizing: border-box;
}

</style>
