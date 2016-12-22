<template>
  <div class="movie-info">
    <div class="triangle" v-bind:class="'triangle-' + index">
      <div class="inside"></div>
    </div>
    <div class="line"></div>

    <div class="basic-info">
      {{ movie.Genre }} | {{ movie.Runtime }} | {{ movie.Rated }}
    </div>
    <div class="row">
      <div class="plot ten columns">
        {{ movie.Plot }}
      </div>
      <div class="rating two columns">
        <div class="score">
          {{ movie.imdbRating }}/10
        </div>
        <div class="organization">
          IMDB
        </div>
        <div class="score">
          {{ movie.Metascore }}
        </div>
        <div class="organization">
          Metascore
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'movie-info',
  props: ['movie', 'index']
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
.organization {
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
  .basic-info, .plot {
    text-align: left;
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
