<template>
  <div class="container movies">
    <div class="row">
      <h2>Results for: {{ searchInput }}</h2>
    </div>
    <div class="row">
      <div class="three columns" v-for="movie in movies">
        {{ movie.title }}
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
</style>
