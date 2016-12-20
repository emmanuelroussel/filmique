<template>
  <div id="app">
    <home v-on:search="search"></home>
    <search-result v-if="results.length > 0" :movies="results" :search-input="searchInput"></search-result>
  </div>
</template>

<script>
import Home from './components/Home'
import SearchResult from './components/SearchResult'

export default {
  name: 'app',
  components: {
    Home,
    SearchResult
  },
  data: function () {
    return {
      searchInput: '',
      results: []
    }
  },
  methods: {
    search: function (input) {
      this.searchInput = input

      // Do search
      this.$http.get('http://localhost:3000/api/movies/' + input + '/' + '1').then(function (res) {
        this.results = res.body.results
      }, function (err) {
        console.error(err)
      })
    }
  }
}
</script>

<style src="assets/css/normalize.css"></style>
<style src="assets/css/skeleton.css"></style>
