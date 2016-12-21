<template>
  <div class="movie-info">
    <div class="triangle" v-bind:class="'triangle-' + index">
      <div class="inside"></div>
    </div>
    <div class="line"></div>

    <div class="main">
      {{ movie.Genre }} | {{ movie.Runtime }} | {{ movie.Rated }}
    </div>
    <div class="overview">
      {{ movie.Plot }}
    </div>
    <div class="rating">
        {{ movie.imdbRating }}/10
        <br />
        IMDB
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
.triangle-0 {
  /* margin-left: -moz-calc(12.5% - 25px - 0.5em);
  margin-left: -webkit-calc(12.5% - 25px - 0.5em);
  margin-left: -o-calc(12.5% - 25px - 0.5em); */
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
.line {
  border-bottom: 1px solid red;
  margin-bottom: 1em;
}
.movie-info {
  display: inline-block;
  width: calc(100% - 2em);
  margin-top: 1em;
  margin-left: 1em;
  margin-right: 1em;
}
.main, .rating {
  font-weight: bold;
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
