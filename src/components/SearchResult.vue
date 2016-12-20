<template>
  <div class="container movies">
    <div class="row">
      <h3>Results for: {{ searchInput }}</h3>
    </div>
    <div class="row grid">
      <div class="custom-column" v-for="movie in movies">
        <div class="grid-inner-container">
          <div class="movie-poster">
            <img class="u-full-width" v-bind:src="movie.poster_path" />
          </div>
          <div class="movie-title">
            {{ movie.title }}
          </div>
          <div>
            {{ movie.release_date | getYear }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'search-result',
  props: ['movies', 'searchInput'],
  filters: {
    getYear: function (date) {
      if (!date) return ''
      return date.slice(0, date.indexOf('-'))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.movie-title {
  font-weight: bold;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.grid {
  text-align: center;
  margin-left: -1em;
  margin-right: -1em;
}
.movie-poster {
  padding-top: 150%;
  position: relative;
  margin-top: -1em;
}
.movie-poster > img {
  position: absolute;
  padding-left: 1em;
  padding-right: 1em;
  padding-top: 2em;
  height: 100%;
  left: 0;
  top: 0;
}
/* Larger than phablet */
@media (min-width: 1000px) {
  .grid {
    margin-left: -2em;
    margin-right: -2em;
  }
  .movie-poster {
    margin-top: -2em;
  }
  .movie-poster > img {
    padding-left: 2em;
    padding-right: 2em;
    padding-top: 4em;
  }
}
</style>
