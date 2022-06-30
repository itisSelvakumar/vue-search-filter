<template>
  <div id="app">
    <Search msg="Search"/>
    <FilterComponent msg="Search + Filter"/>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import FilterComponent from './components/Filter.vue'

export default {
  name: 'App',
  components: {
    Search,
    FilterComponent
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
