<template>
  <div class="container movies">
    <div class="row">
      <h3>Results for: {{ searchInput }}</h3>
    </div>
    <div class="row grid">
      <div v-for="(movie, index) in movies" v-bind:id="'movie-' + index">
        <div class="custom-column" v-on:click="toggleInfo(movie, index)">
          <movie-thumbnail :posterPath="movie.poster_path" :title="movie.title" :releaseDate="movie.release_date"></movie-thumbnail>
        </div>
      </div>
    </div>
    <movie-info v-show="selectedMovie.show" id="movie-info" :movie="selectedMovie.info" :index="selectedMovie.index % 4"></movie-info>
  </div>
</template>

<script>
import MovieInfo from './MovieInfo'
import MovieThumbnail from './MovieThumbnail'
import $ from 'jquery'

export default {
  name: 'search-result',
  components: {
    MovieInfo,
    MovieThumbnail
  },
  props: ['movies', 'searchInput'],
  data: function () {
    return {
      selectedMovie: {
        info: this.movies[0], // dummy data to avoid undefined properties
        index: 0,
        show: false
      }
    }
  },
  methods: {
    toggleInfo: function (movie, index) {
      if (index === this.selectedMovie.index) {
        this.selectedMovie.show = !this.selectedMovie.show
      } else {
        let gridWidth = 2

        if (window.innerWidth > 750) {
          gridWidth = 4
        }

        // Find where the movie-info component should go
        const movieInfoIndex = (Math.ceil((index + 1) / gridWidth) * gridWidth) - 1

        this.$http.get('http://localhost:3000/api/movies/' + movie.id).then(function (res) {
          this.selectedMovie.info = res.body
          this.selectedMovie.index = index

          // Move movie-info component to the right position in the DOM
          $(this.$el).find('#movie-' + movieInfoIndex).append($('#movie-info'))

          this.selectedMovie.show = true
        }, function (err) {
          console.error(err)
        })
      }
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
