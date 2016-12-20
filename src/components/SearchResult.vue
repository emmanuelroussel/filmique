<template>
  <div class="container movies">
    <div class="row">
      <h3>Results for: {{ searchInput }}</h3>
    </div>
    <div class="row grid">
      <div class="custom-column" v-for="(movie, index) in movies" v-on:click="toggleInfo(index)" v-bind:id="'movie-' + index">
        <movie-thumbnail :poster-path="movie.poster_path" :title="movie.title" :release-date="movie.release_date"></movie-thumbnail>
      </div>
    </div>
  </div>
</template>

<script>
import MovieThumbnail from './MovieThumbnail'

export default {
  name: 'search-result',
  components: {
    MovieThumbnail
  },
  props: ['movies', 'searchInput'],
  methods: {
    toggleInfo: function (index) {
      console.log(index)
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
/* Larger than phablet */
@media (min-width: 1000px) {
  .grid {
    margin-left: -2em;
    margin-right: -2em;
  }
}
</style>
