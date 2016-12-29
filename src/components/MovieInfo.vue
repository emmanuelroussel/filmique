<template>
  <div class="movie-info">
    <div class="triangle" v-bind:class="'triangle-' + gridPosition">
      <div class="inside"></div>
    </div>
    <div class="line"></div>

    <div v-show="!loading">
      <div class="row basic-info">
        <span v-show="isSomething(movie.Genre)">{{ movie.Genre }}</span>
        <span v-show="isSomething(movie.Runtime)"> | {{ formattedRuntime }}</span>
        <span v-show="isSomething(movie.Rated)"> | {{ movie.Rated }}</span>
      </div>
      <div class="row">
        <div class="plot ten columns">
          {{ movie.Plot }}
        </div>
        <div class="rating two columns">
          <div v-show="isSomething(movie.imdbRating)">
            <div class="score">
              {{ movie.imdbRating }}/10
            </div>
            <div class="organization">
              IMDB
            </div>
          </div>
          <div v-show="isSomething(movie.tomatoMeter)">
            <div class="score">
              {{ movie.tomatoMeter }}%
            </div>
            <div class="organization">
              Rotten Tomatoes
            </div>
          </div>
        </div>
      </div>
      <div class="row links">
        <a v-show="isSomething(movie.imdbID)" v-bind:href="'http://www.imdb.com/title/' + movie.imdbID" target="_blank">Look it up on IMDb</a>
      </div>
    </div>

    <img class="loading" v-show="loading" src="../assets/rolling.svg" />
  </div>
</template>

<script>
export default {
  name: 'movie-info',
  props: ['movie', 'gridPosition', 'loading'],
  computed: {
    formattedRuntime: function () {
      if (!this.isSomething(this.movie.Runtime)) {
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
  },
  methods: {
    isSomething: function (element) {
      return element && element !== 'N/A'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.movie-info {
  display: inline-block;
  width: calc(100% - 2em);
  margin-top: 1em;
  margin-left: 1em;
  margin-right: 1em;
}
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
.basic-info {
  margin-bottom: 0.5em;
}
.basic-info, .score {
  font-weight: bold;
}
.rating > div {
  line-height: normal;
  width: 45%;
  display: inline-block;
}
.organization {
  margin-bottom: 1em;
}
.rating, .loading {
  margin-top: 1em;
}
.loading {
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
