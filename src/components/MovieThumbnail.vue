<template>
  <div >
    <div class="movie-poster">
      <img class="u-full-width" v-bind:src="poster" />
    </div>
    <div class="movie-title">
      {{ title }}
    </div>
    <div>
      {{ date | getYear }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'movie-thumbnail',
  props: ['poster', 'title', 'date'],
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
.movie-poster {
  padding-top: 150%;
  position: relative;
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
  .movie-poster > img {
    padding-left: 2em;
    padding-right: 2em;
    padding-top: 4em;
  }
}
</style>
