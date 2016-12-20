<template>
  <div class="movie-info">
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
.main, .rating {
  font-weight: bold;
}
</style>
