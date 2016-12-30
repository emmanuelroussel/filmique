<template>
  <div>
    <div class="poster">
      <img class="u-full-width" v-bind:src="posterPath" />
    </div>
    <div class="title">
      {{ title }}
    </div>
    <div class="release-date">
      {{ releaseDate | getYear }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'movie',
  props: ['posterPath', 'title', 'releaseDate'],
  filters: {
    getYear: function (date) {
      if (!date) return '-'
      return date.slice(0, date.indexOf('-'))
    }
  },
  methods: {
    toggleInfo: function () {
      this.$emit('toggleInfo', this.input)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title {
  font-weight: bold;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  margin-top: 0.5em;
}
.release-date {
  line-height: 1;
}
.poster {
  padding-top: 150%;
  position: relative;
}
.poster > img {
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
  .poster > img {
    padding-left: 2em;
    padding-right: 2em;
    padding-top: 4em;
  }
}
</style>
