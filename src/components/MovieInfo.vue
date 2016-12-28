<template>
  <div class="movie-info">
    <div class="triangle" v-bind:class="'triangle-' + index">
      <div class="inside"></div>
    </div>
    <div class="line"></div>

    <div v-show="!loading">
      <div class="basic-info">
        <span v-show="movie.Genre && movie.Genre !== 'N/A'">{{ movie.Genre }}</span>
        <span v-show="movie.Runtime && movie.Runtime !== 'N/A'"> | {{ formattedRuntime }}</span>
        <span v-show="movie.Rated && movie.Rated !== 'N/A'"> | {{ movie.Rated }}</span>
      </div>
      <div class="row">
        <div class="plot ten columns">
          {{ movie.Plot }}
        </div>
        <div class="rating two columns">
          <div v-show="movie.imdbRating && movie.imdbRating !== 'N/A'">
            <div class="score">
              {{ movie.imdbRating }}/10
            </div>
            <div class="organization">
              IMDB
            </div>
          </div>
          <div v-show="movie.tomatoMeter && movie.tomatoMeter !== 'N/A'">
            <div class="score">
              {{ movie.tomatoMeter }}%
            </div>
            <div class="organization">
              Rotten Tomatoes
            </div>
          </div>
        </div>
      </div>
      <div class="links row">
        <a v-show="movie.imdbID" v-bind:href="'http://www.imdb.com/title/' + movie.imdbID" target="_blank">Look it up on IMDb</a>
      </div>
    </div>
    <img class="loading" v-show="loading" src="../assets/rolling.svg" />
  </div>
</template>

<script>
export default {
  name: 'movie-info',
  props: ['movie', 'index', 'loading'],
  computed: {
    formattedRuntime: function () {
      if (!this.movie.Runtime || this.movie.Runtime === 'N/A') {
        return ''
      }

      const runtime = this.movie.Runtime.replace(' min', '')
      const hours = Math.floor(runtime / 60)
      let minutes = runtime % 60

      if (minutes < 10) {
        minutes = '0' + minutes
      }
      return hours + 'h ' + minutes
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.inside, .triangle {
  width: 0;
	height: 0;
  border-left: 25px solid transparent;
	border-right: 25px solid transparent;
}
.inside {
  position: absolute;
	border-bottom: 20px solid #FFF;
  left: -25px;
  top: 1px;
}
.triangle {
  position: relative;
	border-bottom: 20px solid #F2545B;
}
.triangle-0, .triangle-2 {
  margin-left: calc(((50% - 1em) / 2) - 25px);
}
.triangle-1, .triangle-3 {
  margin-left: calc(100% - ((50% - 1em) / 2) - 25px);
}
.line {
  border-bottom: 1px solid red;
  margin-bottom: 0.5em;
}
.movie-info {
  display: inline-block;
  width: calc(100% - 2em);
  margin-top: 1em;
  margin-left: 1em;
  margin-right: 1em;
}
.basic-info {
  margin-bottom: 0.5em;
}
.basic-info, .score {
  font-weight: bold;
}
.rating {
  line-height: normal;
}
.rating > div {
  width: 45%;
  display: inline-block;
}
.organization {
  margin-bottom: 1em;
}
.rating {
  margin-top: 1em;
}
.loading {
  margin-top: 1em;
  margin-bottom: 1em;
}
/* Larger than tablet */
@media (min-width: 750px) {
  .triangle-0 {
    margin-left: calc(((100% - 6em) / 8) - 25px);
  }
  .triangle-1 {
    margin-left: calc((((100% - 6em) / 8) * 3) - 25px + 2em);
  }
  .triangle-2 {
    margin-left: calc((((100% - 6em) / 8) * 5) - 25px + 4em);
  }
  .triangle-3 {
    margin-left: calc((((100% - 6em) / 8) * 7) - 25px + 6em);
  }
  .basic-info, .plot, .links {
    text-align: left;
  }
  .rating {
    margin-top: 0;
    right: 0;
    position: absolute;
  }
  .rating > div {
    width: auto;
    display: block;
  }
  .links {
    margin-top: 1em;
  }
}
/* Larger than phablet */
@media (min-width: 1000px) {
  .movie-info {
    margin-left: 2em;
    margin-right: 2em;
    width: calc(100% - 4em);
  }
  .triangle-0 {
    margin-left: calc(((100% - 12em) / 8) - 25px);
  }
  .triangle-1 {
    margin-left: calc((((100% - 12em) / 8) * 3) - 25px + 4em);
  }
  .triangle-2 {
    margin-left: calc((((100% - 12em) / 8) * 5) - 25px + 8em);
  }
  .triangle-3 {
    margin-left: calc((((100% - 12em) / 8) * 7) - 25px + 12em);
  }
}
</style>
