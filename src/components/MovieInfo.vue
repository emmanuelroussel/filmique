<template>
  <div class="movie-info">
    {{ movie.overview }}
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

</style>
