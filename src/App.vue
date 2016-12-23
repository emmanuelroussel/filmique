<template>
  <div id="app">
    <home v-on:search="search"></home>
    <search-result v-if="results.length > 0" :movies="results" :search-input="searchInput" v-on:scroll="scroll"></search-result>
    <footer v-if="results.length > 0" >
      <img src="./assets/powered-by-tmdb.svg" />
      <p>This product uses the TMDb API but is not endorsed or certified by TMDb</p>
    </footer>
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
      this.results = []
      this.searchInput = input

      // Do search
      this.$http.get('http://localhost:3000/api/movies/search', {
        params: {
          search: input,
          page: 1
        }
      }).then(function (res) {
        // Add info = false to all movies
        let tempResults = res.body.results
        if (tempResults) {
          for (let i = 0; i < tempResults.length; i++) {
            tempResults[i].info = false
          }
        }

        this.results = tempResults
      }, function (err) {
        console.error(err)
      })
    },
    scroll: function () {
      this.$http.get('http://localhost:3000/api/movies/search', {
        params: {
          search: this.searchInput,
          page: this.results.length / 20 + 1
        }
      }).then(function (res) {
        console.log(res)
        if (res.body.results) {
          this.results = this.results.concat(res.body.results)
          this.$refs.infiniteLoading.$emit('$InfiniteLoading:loaded')
        } else {
          this.$refs.infiniteLoading.$emit('$InfiniteLoading:complete')
        }
      }, function (err) {
        console.error(err)
      })
    }
  }
}
</script>

<style src="assets/css/normalize.css"></style>
<style src="assets/css/skeleton.css"></style>
<style scoped>

footer {
  margin-top: 8em;
  margin-bottom: 2em;
  text-align: center;
  font-size: 1.2rem;
}
footer img {
  width: 100px;
  margin: 0 auto;
}
</style>
