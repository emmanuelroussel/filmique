<template>
  <div class="container movies">
    <div class="row">
      <h3>Results for: {{ searchInput }}</h3>
    </div>
    <div class="row grid">
      <div class="custom-column" v-for="(item, index) in items" v-on:click="toggleInfo(item, index)" v-bind:class="{ 'movie-info-container': item.info }">
        <movie-info v-if="item.info" :movie="item" :index="item.index"></movie-info>
        <movie-thumbnail v-else :poster="item.poster_path" :title="item.title" :date="item.release_date"></movie-thumbnail>
      </div>
    </div>
  </div>
</template>

<script>
import MovieInfo from './MovieInfo'
import MovieThumbnail from './MovieThumbnail'

export default {
  name: 'search-result',
  components: {
    MovieInfo,
    MovieThumbnail
  },
  props: ['movies', 'searchInput'],
  data: function () {
    return {
      items: this.movies
    }
  },
  methods: {
    toggleInfo: function (movie, index) {
      this.$http.get('http://localhost:3000/api/movies/' + movie.id).then(function (res) {
        let movieInfo = res.body
        movieInfo.info = true
        movieInfo.index = index
        this.items.splice(Math.ceil((index + 1) / 4.0) * 4, 0, movieInfo)
        console.log(this.items[Math.ceil((index + 1) / 4.0) * 4])
      }, function (err) {
        console.error(err)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.grid {
  text-align: center;
  margin-left: -1em;
  margin-right: -1em;
}
.movie-info-container {
  width: 100%;
}
/* Larger than phablet */
@media (min-width: 1000px) {
  .grid {
    margin-left: -2em;
    margin-right: -2em;
  }
}
</style>
