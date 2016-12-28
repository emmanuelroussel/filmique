<template>
  <div id="app">
    <home v-on:search="search" v-on:inputChange="resetErrorMessage" :error="error" :loading="loading.search"></home>
    <search-result v-if="results.length > 0" :movies="results" :search-input="searchInput"></search-result>
    <infinite-loading :on-infinite="onInfinite" ref="infiniteLoading" v-if="results.length > 0" spinner="spiral">
      <span slot="no-more"></span>
      <span slot="no-results"></span>
    </infinite-loading>
    <footer v-if="results.length > 0" >
      <img src="./assets/powered-by-tmdb.svg" />
      <p>This product uses the TMDb API but is not endorsed or certified by TMDb</p>
    </footer>
  </div>
</template>

<script>
import Home from './components/Home'
import SearchResult from './components/SearchResult'
import InfiniteLoading from 'vue-infinite-loading'

export default {
  name: 'app',
  components: {
    Home,
    SearchResult,
    InfiniteLoading
  },
  data: function () {
    return {
      searchInput: '',
      results: [],
      page: 1,
      error: '',
      loading: {
        search: false,
        info: false
      }
    }
  },
  methods: {
    search: function (input) {
      this.loading.search = true
      this.results = []
      this.searchInput = input
      this.page = 1

      // Do search
      this.$http.get('http://localhost:3000/api/movies/search', {
        params: {
          search: input,
          page: this.page
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
        if (err.status === 404) {
          this.error = 'Sorry, no movies found for: ' + this.searchInput
        } else if (err.status === 500) {
          this.error = 'Oups something went wrong'
        }
      }).finally(function () {
        this.loading.search = false
      })
    },
    resetErrorMessage: function () {
      this.error = ''
    },
    onInfinite: function () {
      this.page ++

      this.$http.get('http://localhost:3000/api/movies/search', {
        params: {
          search: this.searchInput,
          page: this.page
        }
      }).then(function (res) {
        if (res.body.results.length) {
          this.results = this.results.concat(res.body.results)
          this.$refs.infiniteLoading.$emit('$InfiniteLoading:loaded')
        } else {
          this.$refs.infiniteLoading.$emit('$InfiniteLoading:complete')
        }
      }, function (err) {
        console.error(err)
        if (err.status === 404) {
          this.$refs.infiniteLoading.$emit('$InfiniteLoading:complete')
        }
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

<style>
.loading-spiral {
  border-color: #F2545B !important;
  border-right-color: transparent !important;
}
</style>
