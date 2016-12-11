<template>
  <div id="app">
    <home v-on:search="search"></home>
  </div>
</template>

<script>
import Home from './components/Home'

export default {
  name: 'app',
  components: {
    Home
  },
  data: function () {
    return {
      searchInput: 'Hello'
    }
  },
  methods: {
    search: function (input) {
      this.searchInput = input
    }
  }
}
</script>

<style src="assets/css/normalize.css"></style>
<style src="assets/css/skeleton.css"></style>
