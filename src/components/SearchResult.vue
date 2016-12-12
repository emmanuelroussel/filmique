<template>
  <div class="container movies">
    <div class="row">
      <h3>Results for: {{ searchInput }}</h3>
    </div>
    <div class="row grid">
      <div class="custom-column" v-for="movie in movies">
        <div class="grid-inner-container">
          <img class="u-max-full-width movie-poster" v-bind:src="movie.poster_path" />
          <div class="movie-title">
            {{ movie.title }}
          </div>
          <div>
            {{ movie.release_date }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'search-result',
  props: ['movies', 'searchInput']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.movie-title {
  font-weight: bold;
}
.grid {
  text-align: center;
  margin-left: -1em;
  margin-right: -1em;
}
.movie-poster {
  padding-left: 1em;
  padding-right: 1em;
  padding-top: 1em;
}
/* Larger than phablet */
@media (min-width: 550px) {
  .grid {
    margin-left: -2em;
    margin-right: -2em;
  }
  .movie-poster {
    padding-left: 2em;
    padding-right: 2em;
    padding-top: 2em;
  }
}
</style>
