<template>
  <div class="container movies">
    <div class="row grid">
      <div v-for="(movie, index) in movies" v-bind:id="'movie-' + index">
        <div class="custom-column" v-on:click="toggleInfo(movie, index)">
          <movie :posterPath="movie.poster_path" :title="movie.title" :releaseDate="movie.release_date"></movie>
        </div>
      </div>
    </div>
    <movie-info v-show="selectedMovie.show" id="movie-info" :movie="selectedMovie.info" :gridPosition="selectedMovie.index % 4" :loading="loadingInfo"></movie-info>
  </div>
</template>

<script>
import MovieInfo from './MovieInfo'
import Movie from './Movie'
import $ from 'jquery'

const scrollToMovie = function (index) {
  $('html, body').animate({
    scrollTop: $('#movie-' + index).children('.custom-column').offset().top
  }, 300)
}

export default {
  name: 'movie-grid',
  components: {
    MovieInfo,
    Movie
  },
  props: ['movies'],
  data: function () {
    return {
      selectedMovie: {
        info: this.movies[0], // dummy data to avoid undefined properties
        index: -1,
        show: false
      },
      loadingInfo: false
    }
  },
  methods: {
    toggleInfo: function (movie, index) {
      if (index === this.selectedMovie.index) {
        this.selectedMovie.show = !this.selectedMovie.show

        if (this.selectedMovie.show) {
          scrollToMovie(index)
        }
      } else {
        let gridWidth = 2

        if (window.innerWidth > 750) {
          gridWidth = 4
        }

        // Find where the movie-info component should go in the grid
        let movieInfoIndex = (Math.ceil((index + 1) / gridWidth) * gridWidth) - 1
        if (movieInfoIndex > this.movies.length - 1) {
          movieInfoIndex = this.movies.length - 1
        }

        // Move movie-info component to the right position in the DOM
        const movieContainer = document.getElementById('movie-' + movieInfoIndex)
        const movieInfoElement = document.getElementById('movie-info')
        movieContainer.appendChild(movieInfoElement)

        this.selectedMovie.index = index
        this.loadingInfo = true
        this.selectedMovie.show = true

        scrollToMovie(index)

        this.$http.get(process.env.API_URL + '/movies/' + movie.id).then(function (res) {
          this.selectedMovie.info = res.body
        }, function (err) {
          console.error(err)
        }).finally(function () {
          this.loadingInfo = false
        })
      }
    }
  },
  mounted: function () {
    $('html, body').animate({
      scrollTop: $(this.$el).offset().top
    }, 300)
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
